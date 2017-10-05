---
title: "Azure Otomasyon karma Runbook çalışanını runbook'ları çalıştırmak | Microsoft Docs"
description: "Bu makalede, yerel veri merkezinde veya Bulut sağlayıcısı karma Runbook çalışan rolü ile makinelerde çalışan runbook'ları hakkında bilgi sağlar."
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
ms.openlocfilehash: 993bc3ea480a329541ca4ae825189cdb5a2b4a8b
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="729f8-103">Bir karma Runbook çalışanı üzerinde çalışan runbook'ları</span><span class="sxs-lookup"><span data-stu-id="729f8-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="729f8-104">Azure Automation ve karma Runbook çalışanı üzerinde çalışacak çalışan runbook'ları yapısını fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="729f8-104">There is no difference in the structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="729f8-105">Her ile kullandığınız runbook'ları kaynakları yerel bilgisayarda veya dağıtıldığı, runbook'ları sırasında yerel ortamında kaynaklara karşı bir karma Runbook çalışanı genellikle hedefleyen runbook'ları yönetmek beri büyük olasılıkla ancak önemli ölçüde farklı Azure Otomasyonu, Azure bulut kaynaklarında genellikle yönetin.</span><span class="sxs-lookup"><span data-stu-id="729f8-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on the local computer itself or against resources in the local environment where it is deployed, while runbooks in Azure Automation typically manage resources in the Azure cloud.</span></span>

<span data-ttu-id="729f8-106">Azure Otomasyon karma Runbook çalışanı için bir runbook'u düzenlemek, ancak runbook Düzenleyicisinde test edin çalışırsanız, ilgili sorunlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="729f8-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try to test the runbook in the editor.</span></span>  <span data-ttu-id="729f8-107">Yerel kaynaklar Azure Otomasyonu ortamınızda; bu durumda yüklenmeyebilir erişim PowerShell modülleri, test başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="729f8-107">The PowerShell modules that access the local resources may not be installed in your Azure Automation environment in which case, the test would fail.</span></span>  <span data-ttu-id="729f8-108">Gerekli modüllerini yükleyin, ardından runbook çalışır, ancak tam test için yerel kaynaklara erişmek mümkün olmaz.</span><span class="sxs-lookup"><span data-stu-id="729f8-108">If you do install the required modules, then the runbook will run, but it will not be able to access local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="729f8-109">Karma Runbook çalışanını runbook başlatma</span><span class="sxs-lookup"><span data-stu-id="729f8-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="729f8-110">[Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md) bir runbook'u başlatmak için farklı yöntemleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="729f8-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="729f8-111">Karma Runbook çalışanı ekler bir **RunOn** bir karma Runbook çalışan grubu adını belirtebileceğiniz seçeneği.</span><span class="sxs-lookup"><span data-stu-id="729f8-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify the name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="729f8-112">Bir grubu belirtilirse, ardından runbook alınır ve o grubun çalışanlar tarafından çalıştırılan.</span><span class="sxs-lookup"><span data-stu-id="729f8-112">If a group is specified, then the runbook is retrieved and run by of the workers in that group.</span></span>  <span data-ttu-id="729f8-113">Bu seçenek belirtilmezse, ardından onu Azure Otomasyonu'nda normal olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="729f8-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="729f8-114">Azure portalında bir runbook'u başlattığınızda ile sunulan bir **çalıştıracağınız** seçebileceğiniz seçeneği **Azure** veya **karma çalışanı**.</span><span class="sxs-lookup"><span data-stu-id="729f8-114">When you start a runbook in the Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="729f8-115">Seçerseniz **karma çalışanı**, sonra da aşağı açılır listeden grup seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="729f8-115">If you select **Hybrid Worker**, then you can select the group from a dropdown.</span></span>

<span data-ttu-id="729f8-116">Kullanım **RunOn** parametresi.</span><span class="sxs-lookup"><span data-stu-id="729f8-116">Use the **RunOn** parameter.</span></span>  <span data-ttu-id="729f8-117">Windows PowerShell kullanarak MyHybridGroup adlı bir karma Runbook çalışan grubu üzerinde Test-Runbook adlı bir runbook'u başlatmak için aşağıdaki komutu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="729f8-117">You can use the following command to start a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="729f8-118">**RunOn** parametresi eklendiği **başlangıç AzureAutomationRunbook** 0.9.1 sürümünde Microsoft Azure PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="729f8-118">The **RunOn** parameter was added to the **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="729f8-119">Yapmanız gerekenler [en son sürümü karşıdan](https://azure.microsoft.com/downloads/) yüklü daha önceki bir varsa.</span><span class="sxs-lookup"><span data-stu-id="729f8-119">You should [download the latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="729f8-120">Yalnızca bir iş istasyonunda burada Windows Powershell'den runbook başlatılıyor bu sürümü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="729f8-120">You only need to install this version on a workstation where you are starting the runbook from Windows PowerShell.</span></span>  <span data-ttu-id="729f8-121">Bu bilgisayardan runbook'ları başlatmak düşünmüyorsanız çalışan bilgisayara yüklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="729f8-121">You do not need to install it on the worker computer unless you intend to start runbooks from that computer.</span></span>  <span data-ttu-id="729f8-122">Bu Otomasyon hesabınızda yüklenecek Azure Powershell en son sürümünü gerektirir olduğundan başka bir runbook'tan bir karma Runbook çalışanı üzerinde şu anda bir runbook başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="729f8-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require the latest version of Azure Powershell to be installed in your Automation account.</span></span>  <span data-ttu-id="729f8-123">En son sürümü Azure Otomasyonu'nda otomatik olarak güncelleştirilir ve otomatik olarak çalışanlarına en kısa sürede gönderilen.</span><span class="sxs-lookup"><span data-stu-id="729f8-123">The latest version is automatically updated in Azure Automation and automatically pushed down to the workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="729f8-124">Runbook izinleri</span><span class="sxs-lookup"><span data-stu-id="729f8-124">Runbook permissions</span></span>
<span data-ttu-id="729f8-125">Bir karma Runbook çalışanı üzerinde çalışan runbook'ları, genellikle Azure dışında kaynaklara erişmesi beri runbook'ları Azure kaynakları için kimlik doğrulaması için kullanılan yöntemin kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="729f8-125">Runbooks running on a Hybrid Runbook Worker cannot use the same method that is typically used for runbooks authenticating to Azure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="729f8-126">Runbook yerel kaynakları için kendi kimlik doğrulaması ya da sağlayabilir veya tüm runbook'lar için bir kullanıcı bağlamı sağlamak üzere bir farklı çalıştır hesabı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="729f8-126">The runbook can either provide its own authentication to local resources, or you can specify a RunAs account to provide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="729f8-127">Runbook kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="729f8-127">Runbook authentication</span></span>
<span data-ttu-id="729f8-128">Kendi kimlik doğrulama sunucusuna erişecek kaynaklara sağlamaları gerekir böylece varsayılan olarak, yerel sistem hesabı bağlamında runbook'ları şirket içi bilgisayarda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="729f8-128">By default, runbooks will run in the context of the local System account on the on-premises computer, so they must provide their own authentication to resources that they will access.</span></span>  

<span data-ttu-id="729f8-129">Kullanabileceğiniz [kimlik bilgisi](http://msdn.microsoft.com/library/dn940015.aspx) ve [sertifika](http://msdn.microsoft.com/library/dn940013.aspx) varlıklar runbook'unuzda cmdlet'leri farklı kaynaklarda kimlik doğrulaması için kimlik bilgilerini belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="729f8-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you to specify credentials so you can authenticate to different resources.</span></span>  <span data-ttu-id="729f8-130">Aşağıdaki örnek, bir bilgisayarı yeniden başlatır bir runbook bir kısmı gösterir.</span><span class="sxs-lookup"><span data-stu-id="729f8-130">The following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="729f8-131">Kimlik bilgilerini bir kimlik bilgisi varlığı ve değişken varlığı bilgisayardan adını alır ve ardından bilgisayarı yeniden başlat cmdlet'iyle bu değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="729f8-131">It retrieves credentials from a credential asset and the name of the computer from a variable asset and then uses these values with the Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="729f8-132">Ayrıca yararlanabilirsiniz [Inlinescript](automation-powershell-workflow.md#inlinescript), kod bloklarını tarafından belirtilen kimlik bilgilerine sahip başka bir bilgisayarda çalıştırmanıza olanak sağlayan [PSCredential ortak parametresi](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="729f8-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you to run blocks of code on another computer with credentials specified by the [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="729f8-133">RunAs hesabı</span><span class="sxs-lookup"><span data-stu-id="729f8-133">RunAs account</span></span>
<span data-ttu-id="729f8-134">Belirleyebileceğiniz yerel kaynakları için kendi kimlik doğrulaması runbook'ları sahip olmak yerine bir **RunAs** hesap için bir karma çalışanı grubu.</span><span class="sxs-lookup"><span data-stu-id="729f8-134">Instead of having runbooks provide their own authentication to local resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="729f8-135">Belirttiğiniz bir [kimlik bilgisi varlığı](automation-credentials.md) yerel kaynaklara erişimi olan ve gruptaki bir karma Runbook çalışanı üzerinde çalışan tüm runbook'ları bu kimlik bilgileri altında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="729f8-135">You specify a [credential asset](automation-credentials.md) that has access to local resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in the group.</span></span>  

<span data-ttu-id="729f8-136">Kullanıcı adı kimlik bilgisi için aşağıdaki biçimlerden birinde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="729f8-136">The user name for the credential must be in one of the following formats:</span></span>

* <span data-ttu-id="729f8-137">etki alanı\kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="729f8-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="729f8-138">Kullanıcı adı (için hesapları şirket içi bilgisayarın yerel)</span><span class="sxs-lookup"><span data-stu-id="729f8-138">username (for accounts local to the on-premises computer)</span></span>

<span data-ttu-id="729f8-139">Karma çalışanı grubu için bir RunAs hesabı belirtmek için aşağıdaki yordamı kullanın:</span><span class="sxs-lookup"><span data-stu-id="729f8-139">Use the following procedure to specify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="729f8-140">Oluşturma bir [kimlik bilgisi varlığı](automation-credentials.md) yerel kaynaklara erişim.</span><span class="sxs-lookup"><span data-stu-id="729f8-140">Create a [credential asset](automation-credentials.md) with access to local resources.</span></span>
2. <span data-ttu-id="729f8-141">Azure Portal'da Automation hesabını açın.</span><span class="sxs-lookup"><span data-stu-id="729f8-141">Open the Automation account in the Azure portal.</span></span>
3. <span data-ttu-id="729f8-142">Seçin **karma çalışan grupları** döşeme ve grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="729f8-142">Select the **Hybrid Worker Groups** tile, and then select the group.</span></span>
4. <span data-ttu-id="729f8-143">Seçin **tüm ayarları** ve ardından **karma çalışanı grubu ayarları**.</span><span class="sxs-lookup"><span data-stu-id="729f8-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="729f8-144">Değişiklik **Farklı Çalıştır** gelen **varsayılan** için **özel**.</span><span class="sxs-lookup"><span data-stu-id="729f8-144">Change **Run As** from **Default** to **Custom**.</span></span>
6. <span data-ttu-id="729f8-145">Kimlik bilgisi seçin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="729f8-145">Select the credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="729f8-146">Automation farklı çalıştır hesabı</span><span class="sxs-lookup"><span data-stu-id="729f8-146">Automation Run As account</span></span>
<span data-ttu-id="729f8-147">Azure'daki kaynakların dağıtımı için otomatik yapı işleminizin bir parçası olarak, şirket içi bir görev veya grup adımı, dağıtım sırası desteklemek üzere sistemler için erişim gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="729f8-147">As part of your automated build process for deploying resources in Azure, you may require access to on-premise systems to support a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="729f8-148">Azure farklı çalıştır hesabını kullanarak kimlik doğrulamasını desteklemek için farklı çalıştır hesabı sertifikası yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="729f8-148">To support authentication against Azure using the Run As account, you need to install the Run As account certificate.</span></span>  

<span data-ttu-id="729f8-149">Aşağıdaki PowerShell runbook *verme RunAsCertificateToHybridWorker*, Azure Automation hesabınızdan farklı çalıştır sertifika verir ve indirir ve bunu bir karma yerel makine sertifika deposuna aktarır çalışan aynı hesaba bağlı.</span><span class="sxs-lookup"><span data-stu-id="729f8-149">The following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports the Run As certificate from your Azure Automation account and downloads and imports it into the local machine certificate store on a Hybrid worker connected to the same account.</span></span>  <span data-ttu-id="729f8-150">Bu adım tamamlandıktan sonra çalışan farklı çalıştır hesabını kullanarak Azure kimlik doğrulamasını başarıyla doğrular.</span><span class="sxs-lookup"><span data-stu-id="729f8-150">Once that step is completed, it verifies the worker can successfully authenticate to Azure using the Run As account.</span></span>

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
    Exports the Run As certificate from an Azure Automation account to a hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports the Run As certificate from an Azure Automation account to a hybrid worker in that account.
    Run this runbook in the hybrid worker where you want the certificate installed.
    This allows the use of the AzureRunAsConnection to authenticate to Azure and manage Azure resources from runbooks running in the hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set the password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get the management certificate that will be used to make calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location to store temporary certificate in the Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save the certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication to Azure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts to confirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="729f8-151">Kaydet *verme RunAsCertificateToHybridWorker* runbook bilgisayarınıza bir `.ps1` uzantısı.</span><span class="sxs-lookup"><span data-stu-id="729f8-151">Save the *Export-RunAsCertificateToHybridWorker* runbook to your computer with a `.ps1` extension.</span></span>  <span data-ttu-id="729f8-152">Otomasyon hesabınızda içeri aktarın ve değişkenin değerini değiştirerek bu runbook'u düzenlemek `$Password` kendi parolanızı ile.</span><span class="sxs-lookup"><span data-stu-id="729f8-152">Import it into your Automation account and edit the runbook, changing the value of the variable `$Password` with your own password.</span></span>  <span data-ttu-id="729f8-153">Yayımlama ve çalıştıran ve runbook'ları farklı çalıştır hesabını kullanarak kimlik doğrulaması karma çalışanı grubu hedefleme runbook çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="729f8-153">Publish and then run the runbook targeting the Hybrid Worker group that run and authenticate runbooks using the Run As account.</span></span>  <span data-ttu-id="729f8-154">İş akışı yerel makine deposuna sertifika alma girişimi raporları ve kaç tane Automation hesapları aboneliğinizde tanımlanır ve kimlik doğrulaması başarılı olup olmadığını bağlı olarak birden fazla satır ile izler.</span><span class="sxs-lookup"><span data-stu-id="729f8-154">The job stream reports the attempt to import the certificate into the local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="729f8-155">Karma Runbook çalışanı runbook'larda sorun giderme</span><span class="sxs-lookup"><span data-stu-id="729f8-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="729f8-156">Günlükleri yerel olarak her karma çalışanı C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes konumunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="729f8-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="729f8-157">Karma çalışanı de kaydeder hatalarını ve olaylarını Windows olay günlüğünde altında **uygulama ve Hizmetleri Logs\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="729f8-157">Hybrid worker also records errors and events in the Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="729f8-158">Çalışan üzerinde yürütülen runbook'ları ilgili olayları için yazılır **uygulama ve Hizmetleri Logs\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="729f8-158">Events related to runbooks executed on the worker are written to **Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="729f8-159">**Microsoft SMA** günlük çalışan ve runbook işleme gönderilen runbook işi ilgili pek çok daha fazla olay içerir.</span><span class="sxs-lookup"><span data-stu-id="729f8-159">The **Microsoft-SMA** log includes many more events related to the runbook job pushed to the worker and the processing of the runbook.</span></span>  <span data-ttu-id="729f8-160">Sırada **Microsoft Otomasyon** olay günlüğü sahip değil birçok olay runbook yürütülmesi gidermeye yardımcı ayrıntılarla ve sonuçları runbook işi, en az bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="729f8-160">While the **Microsoft-Automation** event log does not have many events with details assisting with the troubleshooting of runbook execution, you will at least find the results of the runbook job.</span></span>  

<span data-ttu-id="729f8-161">[Runbook çıkışı ve iletileri](automation-runbook-output-and-messages.md) Azure Otomasyon karma gönderilen bulutta çalışan runbook işleri gibi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="729f8-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent to Azure Automation from hybrid workers just like runbook jobs run in the cloud.</span></span>  <span data-ttu-id="729f8-162">Bu gibi durumlarda, ayrıntılı ve ilerleme akışları ayrıca diğer runbook'lar için olduğu gibi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="729f8-162">You can also enable the Verbose and Progress streams the same way you would for other runbooks.</span></span>  

<span data-ttu-id="729f8-163">Runbook'larınızın başarıyla tamamlanamamasının ve Özet iş durumunu gösterir **askıya**, lütfen sorun giderme makalesi gözden [karma Runbook çalışanı: bir runbook işi askıya alındı durumu ile sona erer ](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="729f8-163">If your runbooks are not completing successfully and the job summary shows a status of **Suspended**, please review the troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="729f8-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="729f8-164">Next steps</span></span>
* <span data-ttu-id="729f8-165">Bir runbook'u başlatmak için kullanılan farklı yöntemleri hakkında daha fazla bilgi için bkz: [Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="729f8-165">To learn more about the different methods that can be used to start a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="729f8-166">PowerShell ve PowerShell iş akışı runbook'ları metin düzenleyicisini kullanarak Azure Automation ile çalışmak için farklı yordamlar anlamak için bkz: [Azure Otomasyon Runbook'u düzenleme](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="729f8-166">To understand the different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using the textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>