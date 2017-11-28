---
title: "Azure Otomasyonu DSC yapılandırmalarında aaaCompiling | Microsoft Docs"
description: "Bu makalede nasıl toocompile istenen durum Yapılandırması'nı (DSC) yapılandırmaları Azure Automation için."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="a239f-103">Azure Otomasyonu DSC yapılandırmalarında derleme</span><span class="sxs-lookup"><span data-stu-id="a239f-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="a239f-104">İstenen durum Yapılandırması'nı (DSC) yapılandırmaları Azure Automation iki yolla derleyebilirsiniz: hello Azure portalı ve Windows PowerShell ile.</span><span class="sxs-lookup"><span data-stu-id="a239f-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in hello Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="a239f-105">Merhaba aşağıdaki tabloda, ne zaman belirlemenize yardımcı hangi yöntemi her hello özelliklerine göre toouse:</span><span class="sxs-lookup"><span data-stu-id="a239f-105">hello following table will help you determine when toouse which method based on hello characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="a239f-106">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="a239f-106">Azure portal</span></span>

* <span data-ttu-id="a239f-107">Etkileşimli kullanıcı arabirimi ile basit yöntemi</span><span class="sxs-lookup"><span data-stu-id="a239f-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="a239f-108">Form tooprovide basit parametre değerleri</span><span class="sxs-lookup"><span data-stu-id="a239f-108">Form tooprovide simple parameter values</span></span>
* <span data-ttu-id="a239f-109">İş durumu kolayca izleme</span><span class="sxs-lookup"><span data-stu-id="a239f-109">Easily track job state</span></span>
* <span data-ttu-id="a239f-110">İle Azure oturum açma kimliği doğrulanmış erişim</span><span class="sxs-lookup"><span data-stu-id="a239f-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="a239f-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a239f-111">Windows PowerShell</span></span>

* <span data-ttu-id="a239f-112">Windows PowerShell cmdlet'leri ile komut satırından çağırma</span><span class="sxs-lookup"><span data-stu-id="a239f-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="a239f-113">Birden çok adımı otomatik Çözümle eklenebilir</span><span class="sxs-lookup"><span data-stu-id="a239f-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="a239f-114">Basit ve karmaşık parametre değerlerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="a239f-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="a239f-115">İş durumu izleme</span><span class="sxs-lookup"><span data-stu-id="a239f-115">Track job state</span></span>
* <span data-ttu-id="a239f-116">Gerekli istemci toosupport PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="a239f-116">Client required toosupport PowerShell cmdlets</span></span>
* <span data-ttu-id="a239f-117">Geçişi ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="a239f-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="a239f-118">Kimlik bilgilerini kullanan yapılandırmaları derleme</span><span class="sxs-lookup"><span data-stu-id="a239f-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="a239f-119">Bir derleme yöntem karar verdikten sonra toostart derleme aşağıda hello ilgili yordamları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a239f-119">Once you have decided on a compilation method, you can follow hello respective procedures below toostart compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a><span data-ttu-id="a239f-120">DSC yapılandırması hello Azure portal ile derleme</span><span class="sxs-lookup"><span data-stu-id="a239f-120">Compiling a DSC Configuration with hello Azure portal</span></span>

1. <span data-ttu-id="a239f-121">Otomasyon hesabınızdan tıklatın **DSC yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="a239f-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="a239f-122">Bir yapılandırma tooopen kendi dikey tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a239f-122">Click a configuration tooopen its blade.</span></span>
3. <span data-ttu-id="a239f-123">Tıklatın **derleme**.</span><span class="sxs-lookup"><span data-stu-id="a239f-123">Click **Compile**.</span></span>
4. <span data-ttu-id="a239f-124">Merhaba yapılandırma hiçbir parametrelere sahipse, toocompile istediğinizi istendiğinde tooconfirm olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a239f-124">If hello configuration has no parameters, you will be prompted tooconfirm whether you want toocompile it.</span></span> <span data-ttu-id="a239f-125">Merhaba yapılandırma parametrelere sahipse, hello **derleme yapılandırma** parametre değerlerini sağlayabilmesi için dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="a239f-125">If hello configuration has parameters, hello **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="a239f-126">Merhaba bkz [ **temel parametreleri** ](#basic-parameters) bölümünde aşağıdaki parametreler hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="a239f-126">See hello [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="a239f-127">Merhaba **derleme işi** hello derleme işin durumunu izleyebilir ve hello düğüm yapılandırmaları (MOF yapılandırma belgeler) Azure Automation DSC çekme sunucusuna hello üzerinde yerleştirilen toobe neden dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="a239f-127">hello **Compilation Job** blade is opened so that you can track hello compilation job's status, and hello node configurations (MOF configuration documents) it caused toobe placed on hello Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="a239f-128">DSC Yapılandırması Windows PowerShell ile derleme</span><span class="sxs-lookup"><span data-stu-id="a239f-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="a239f-129">Kullanabileceğiniz [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart Windows PowerShell ile derleme.</span><span class="sxs-lookup"><span data-stu-id="a239f-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compiling with Windows PowerShell.</span></span> <span data-ttu-id="a239f-130">Aşağıdaki örnek kod hello başlatır adlı bir DSC yapılandırma derlenmesini **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="a239f-130">hello following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="a239f-131">`Start-AzureRmAutomationDscCompilationJob`derleme döndürür durumunu tootrack kullanabileceğiniz nesne işi.</span><span class="sxs-lookup"><span data-stu-id="a239f-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use tootrack its status.</span></span> <span data-ttu-id="a239f-132">Bu derleme iş nesnesi ile sonra kullanabileceğiniz [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello hello derleme işi durumunu ve [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview kendi akışlar (çıktı).</span><span class="sxs-lookup"><span data-stu-id="a239f-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello status of hello compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview its streams (output).</span></span> <span data-ttu-id="a239f-133">Aşağıdaki örnek kod hello başlatır hello derlenmesini **SampleConfig** yapılandırması tamamlandı ve onun akışları görüntüler kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="a239f-133">hello following sample code starts compilation of hello **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="a239f-134">Temel parametreleri</span><span class="sxs-lookup"><span data-stu-id="a239f-134">Basic Parameters</span></span>
<span data-ttu-id="a239f-135">DSC yapılandırmaları, parametre türleri ve özellikler, works dahil olmak üzere parametresi bildiriminde hello aynı Azure Otomasyon çalışma kitabı olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="a239f-135">Parameter declaration in DSC configurations, including parameter types and properties, works hello same as in Azure Automation runbooks.</span></span> <span data-ttu-id="a239f-136">Bkz: [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md) toolearn runbook parametreleri hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="a239f-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toolearn more about runbook parameters.</span></span>

<span data-ttu-id="a239f-137">Merhaba aşağıdaki örnek kullanır adlı iki parametre **FeatureName** ve **olmasına**, toodetermine hello değerlerini hello özelliklerinde **ParametersExample.sample** düğümü derleme sırasında oluşturulan yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="a239f-137">hello following example uses two parameters called **FeatureName** and **IsPresent**, toodetermine hello values of properties in hello **ParametersExample.sample** node configuration, generated during compilation.</span></span>

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

<span data-ttu-id="a239f-138">DSC yapılandırmaları'hello Azure Otomasyonu DSC portalında veya Azure PowerShell ile temel parametrelerini kullanmak hazırlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a239f-138">You can compile DSC Configurations that use basic parameters in hello Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="a239f-139">Portal</span><span class="sxs-lookup"><span data-stu-id="a239f-139">Portal</span></span>

<span data-ttu-id="a239f-140">Merhaba Portalı'nda tıkladıktan sonra parametre değerlerini girebilirsiniz **derleme**.</span><span class="sxs-lookup"><span data-stu-id="a239f-140">In hello portal, you can enter parameter values after clicking **Compile**.</span></span>

![alternatif metin](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="a239f-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a239f-142">PowerShell</span></span>

<span data-ttu-id="a239f-143">PowerShell parametrelerinde gerektiren bir [hashtable](http://technet.microsoft.com/library/hh847780.aspx) burada hello anahtar hello parametre adı ile eşleşen ve hello değerine eşit hello parametre değeri.</span><span class="sxs-lookup"><span data-stu-id="a239f-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key matches hello parameter name, and hello value equals hello parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="a239f-144">PSCredentials parametre olarak geçirme hakkında daha fazla bilgi için bkz: <a href="#credential-assets"> **kimlik bilgisi varlıkları** </a> aşağıda.</span><span class="sxs-lookup"><span data-stu-id="a239f-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="a239f-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="a239f-145">ConfigurationData</span></span>
<span data-ttu-id="a239f-146">**ConfigurationData** tooseparate yapısal PowerShell DSC kullanırken hiçbir ortam belirli yapılandırma yapılandırmasından sağlar.</span><span class="sxs-lookup"><span data-stu-id="a239f-146">**ConfigurationData** allows you tooseparate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="a239f-147">Bkz: ["Ne" PowerShell DSC "nerede" ayırarak](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn hakkında daha fazla **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="a239f-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="a239f-148">Kullanabileceğiniz **ConfigurationData** Azure PowerShell kullanarak Azure Otomasyonu DSC, ancak hello Azure portal derlerken.</span><span class="sxs-lookup"><span data-stu-id="a239f-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in hello Azure portal.</span></span>

<span data-ttu-id="a239f-149">Merhaba aşağıdaki örnek DSC yapılandırmasını kullanan **ConfigurationData** hello aracılığıyla **$ConfigurationData** ve **$AllNodes** anahtar sözcükler.</span><span class="sxs-lookup"><span data-stu-id="a239f-149">hello following example DSC configuration uses **ConfigurationData** via hello **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="a239f-150">Ayrıca hello gerekir [ **xWebAdministration** Modülü](https://www.powershellgallery.com/packages/xWebAdministration/) Bu, örneğin:</span><span class="sxs-lookup"><span data-stu-id="a239f-150">You'll also need hello [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

<span data-ttu-id="a239f-151">PowerShell ile Merhaba DSC yapılandırması yukarıda derleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a239f-151">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="a239f-152">PowerShell aşağıda Hello iki düğüm yapılandırmaları toohello Azure Automation DSC çekme sunucusuna ekler: **ConfigurationDataSample.MyVM1** ve **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="a239f-152">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a><span data-ttu-id="a239f-153">Varlıklar</span><span class="sxs-lookup"><span data-stu-id="a239f-153">Assets</span></span>

<span data-ttu-id="a239f-154">Varlık başvuruları olan hello Azure Otomasyonu DSC yapılandırmaları ve runbook'ları aynı.</span><span class="sxs-lookup"><span data-stu-id="a239f-154">Asset references are hello same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="a239f-155">Daha fazla bilgi için Hello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="a239f-155">See hello following for more information:</span></span>

* [<span data-ttu-id="a239f-156">Sertifikalar</span><span class="sxs-lookup"><span data-stu-id="a239f-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="a239f-157">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="a239f-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="a239f-158">Kimlik Bilgileri</span><span class="sxs-lookup"><span data-stu-id="a239f-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="a239f-159">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="a239f-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="a239f-160">Kimlik bilgisi varlıkları</span><span class="sxs-lookup"><span data-stu-id="a239f-160">Credential Assets</span></span>

<span data-ttu-id="a239f-161">Azure Otomasyonu DSC yapılandırmalarında kullanarak kimlik bilgisi varlıkları başvurabilir sırada **Get-AzureRmAutomationCredential**, kimlik bilgisi varlıkları de geçirilebilir içinde parametreleri aracılığıyla isterseniz.</span><span class="sxs-lookup"><span data-stu-id="a239f-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="a239f-162">Bir yapılandırma parametresi, uzun sürerse **PSCredential** yazın yeniden PSCredential nesnesinin yerine bu parametrenin değeri olarak bir Azure Otomasyonu kimlik bilgisi varlığı toopass hello dize adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="a239f-162">If a configuration takes a parameter of **PSCredential** type, then you need toopass hello string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="a239f-163">Merhaba arka planda hello Azure Otomasyonu kimlik bilgisi varlığı bu ada sahip alınabilir ve toohello yapılandırma geçirildi.</span><span class="sxs-lookup"><span data-stu-id="a239f-163">Behind hello scenes, hello Azure Automation credential asset with that name will be retrieved and passed toohello configuration.</span></span>

<span data-ttu-id="a239f-164">Kimlik bilgileri tutma düğüm yapılandırmaları (MOF yapılandırma belgeler) güvenliğini hello kimlik hello düğüm yapılandırması MOF dosyasındaki şifrelenmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a239f-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting hello credentials in hello node configuration MOF file.</span></span> <span data-ttu-id="a239f-165">Azure Otomasyonu bunu bir adım daha fazla sürer ve hello tüm MOF dosyası şifreler.</span><span class="sxs-lookup"><span data-stu-id="a239f-165">Azure Automation takes this one step further and encrypts hello entire MOF file.</span></span> <span data-ttu-id="a239f-166">Ancak, şu anda, PowerShell DSC, olduğundan kesebilirsiniz düğüm yapılandırması MOF oluşturma sırasında düz metin olarak yüzdelik kimlik bilgilerini toobe için PowerShell DSC Azure Otomasyonu hello tüm MOF dosyası sonra şifreleme bilmiyor söylemelisiniz kendi derleme işi aracılığıyla oluşturma.</span><span class="sxs-lookup"><span data-stu-id="a239f-166">However, currently you must tell PowerShell DSC it is okay for credentials toobe outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting hello entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="a239f-167">PowerShell DSC oluşturulan hello düğüm yapılandırması MOF dosyalarından düz metinde yüzdelik kimlik bilgilerini toobe için uygun olduğunu anlayabilirsiniz kullanarak [ **ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="a239f-167">You can tell PowerShell DSC that it is okay for credentials toobe outputted in plain text in hello generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="a239f-168">Geçmesi `PSDscAllowPlainTextPassword = $true` aracılığıyla **ConfigurationData** hello DSC yapılandırması görünür ve kimlik bilgilerini kullanan her düğüm bloğun adı.</span><span class="sxs-lookup"><span data-stu-id="a239f-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in hello DSC configuration and uses credentials.</span></span>

<span data-ttu-id="a239f-169">Merhaba aşağıdaki örnekte bir Otomasyon kimlik bilgisi varlığı kullanan bir DSC yapılandırması gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a239f-169">hello following example shows a DSC configuration that uses an Automation credential asset.</span></span>

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

<span data-ttu-id="a239f-170">PowerShell ile Merhaba DSC yapılandırması yukarıda derleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a239f-170">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="a239f-171">PowerShell aşağıda Hello iki düğüm yapılandırmaları toohello Azure Automation DSC çekme sunucusuna ekler: **CredentialSample.MyVM1** ve **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="a239f-171">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a><span data-ttu-id="a239f-172">Düğüm yapılandırmaları alma</span><span class="sxs-lookup"><span data-stu-id="a239f-172">Importing node configurations</span></span>

<span data-ttu-id="a239f-173">Ayrıca Azure dışında derlediğiniz düğümü configuratons (MOF dosyalarından) içe aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a239f-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="a239f-174">Bu bir avantajı, o düğümü confiturations imzalanabilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="a239f-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="a239f-175">İmzalı düğüm yapılandırması uygulanan toohello düğümü olan hello yapılandırmayı yetkili bir kaynaktan geldiğinden emin hello DSC aracısı tarafından yönetilen bir düğümde yerel olarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="a239f-175">A signed node configuration is verified locally on a managed node by hello DSC agent, ensuring that hello configuration being applied toohello node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="a239f-176">İçeri aktarma kullanabilirsiniz yapılandırmaları Azure Automation hesabınızda oturumu, ancak Azure Otomasyonu desteklememektedir imzalı yapılandırmaları derleme.</span><span class="sxs-lookup"><span data-stu-id="a239f-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="a239f-177">Bir düğüm yapılandırma dosyası 1 MB tooallow büyük olmalıdır, Azure Automation'a içeri toobe.</span><span class="sxs-lookup"><span data-stu-id="a239f-177">A node configuration file must be no larger than 1 MB tooallow it toobe imported into Azure Automation.</span></span>

<span data-ttu-id="a239f-178">Bilgi edinebilirsiniz nasıl https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module adresindeki toosign düğüm yapılandırmaları.</span><span class="sxs-lookup"><span data-stu-id="a239f-178">You can learn how toosign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a><span data-ttu-id="a239f-179">Bir düğüm yapılandırması hello Azure portal içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="a239f-179">Importing a node configuration in hello Azure portal</span></span>

1. <span data-ttu-id="a239f-180">Otomasyon hesabınızdan tıklatın **DSC düğüm yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="a239f-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![DSC düğüm yapılandırmaları](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="a239f-182">Merhaba, **DSC düğüm yapılandırmaları** dikey penceresinde tıklatın **bir NodeConfiguration eklemek**.</span><span class="sxs-lookup"><span data-stu-id="a239f-182">In hello **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="a239f-183">Merhaba, **alma** dikey penceresinde hello klasör simgesine sonraki toohello tıklatın **düğümü yapılandırma dosyası** textbox toobrowse, yerel bilgisayarınızda bir düğüm yapılandırma dosyası (MOF) için.</span><span class="sxs-lookup"><span data-stu-id="a239f-183">In hello **Import** blade, click hello folder icon next toohello **Node Configuration File** textbox toobrowse for a node configuration file (MOF) on your local computer.</span></span>

    ![Yerel dosya gözatın.](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="a239f-185">Hello bir ad girin **yapılandırma adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a239f-185">Enter a name in hello **Configuration Name** textbox.</span></span> <span data-ttu-id="a239f-186">Bu adı hello düğüm yapılandırması derlenmiş olduğu hello yapılandırmasının hello adıyla eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="a239f-186">This name must match hello name of hello configuration from which hello node configuration was compiled.</span></span>
5. <span data-ttu-id="a239f-187">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a239f-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="a239f-188">Düğüm yapılandırması PowerShell ile içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="a239f-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="a239f-189">Merhaba kullanabilirsiniz [alma AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport Otomasyon hesabınızda bir düğüm yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="a239f-189">You can use hello [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



