---
title: "Azure Otomasyonu DSC yapılandırmalarında derleme | Microsoft Docs"
description: "Bu makalede, Azure Otomasyonu istenen durum Yapılandırması'nı (DSC) yapılandırmaları derlemek açıklar."
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
ms.openlocfilehash: 1aadd604e676659475f00760af3b0bdfb13a4792
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="0a503-103">Azure Otomasyonu DSC yapılandırmalarında derleme</span><span class="sxs-lookup"><span data-stu-id="0a503-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="0a503-104">İstenen durum Yapılandırması'nı (DSC) yapılandırmaları Azure Automation iki yolla derleyebilirsiniz: Azure portalında ve Windows PowerShell ile.</span><span class="sxs-lookup"><span data-stu-id="0a503-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in the Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="0a503-105">Aşağıdaki tabloda, her özelliklerine göre hangi yöntemi kullanmak ne zaman belirlemenize yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="0a503-105">The following table will help you determine when to use which method based on the characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="0a503-106">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="0a503-106">Azure portal</span></span>

* <span data-ttu-id="0a503-107">Etkileşimli kullanıcı arabirimi ile basit yöntemi</span><span class="sxs-lookup"><span data-stu-id="0a503-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="0a503-108">Basit parametre değerlerini sağlamak için form</span><span class="sxs-lookup"><span data-stu-id="0a503-108">Form to provide simple parameter values</span></span>
* <span data-ttu-id="0a503-109">İş durumu kolayca izleme</span><span class="sxs-lookup"><span data-stu-id="0a503-109">Easily track job state</span></span>
* <span data-ttu-id="0a503-110">İle Azure oturum açma kimliği doğrulanmış erişim</span><span class="sxs-lookup"><span data-stu-id="0a503-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="0a503-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a503-111">Windows PowerShell</span></span>

* <span data-ttu-id="0a503-112">Windows PowerShell cmdlet'leri ile komut satırından çağırma</span><span class="sxs-lookup"><span data-stu-id="0a503-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="0a503-113">Birden çok adımı otomatik Çözümle eklenebilir</span><span class="sxs-lookup"><span data-stu-id="0a503-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="0a503-114">Basit ve karmaşık parametre değerlerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="0a503-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="0a503-115">İş durumu izleme</span><span class="sxs-lookup"><span data-stu-id="0a503-115">Track job state</span></span>
* <span data-ttu-id="0a503-116">PowerShell cmdlet'leri desteklemek için gereken istemci</span><span class="sxs-lookup"><span data-stu-id="0a503-116">Client required to support PowerShell cmdlets</span></span>
* <span data-ttu-id="0a503-117">Geçişi ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="0a503-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="0a503-118">Kimlik bilgilerini kullanan yapılandırmaları derleme</span><span class="sxs-lookup"><span data-stu-id="0a503-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="0a503-119">Bir derleme yöntem karar verdikten sonra ilgili derleme başlatmak için aşağıdaki yordamları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a503-119">Once you have decided on a compilation method, you can follow the respective procedures below to start compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-the-azure-portal"></a><span data-ttu-id="0a503-120">DSC yapılandırması Azure portal ile derleme</span><span class="sxs-lookup"><span data-stu-id="0a503-120">Compiling a DSC Configuration with the Azure portal</span></span>

1. <span data-ttu-id="0a503-121">Otomasyon hesabınızdan tıklatın **DSC yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="0a503-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="0a503-122">Kendi dikey penceresini açmak için bir yapılandırma öğesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0a503-122">Click a configuration to open its blade.</span></span>
3. <span data-ttu-id="0a503-123">Tıklatın **derleme**.</span><span class="sxs-lookup"><span data-stu-id="0a503-123">Click **Compile**.</span></span>
4. <span data-ttu-id="0a503-124">Yapılandırma hiçbir parametrelere sahipse, derlemeniz isteyip istemediğinizi onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="0a503-124">If the configuration has no parameters, you will be prompted to confirm whether you want to compile it.</span></span> <span data-ttu-id="0a503-125">Yapılandırma parametreleri, varsa **derleme yapılandırma** parametre değerlerini sağlayabilmesi için dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="0a503-125">If the configuration has parameters, the **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="0a503-126">Bkz: [ **temel parametreleri** ](#basic-parameters) bölümünde aşağıdaki parametreler hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="0a503-126">See the [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="0a503-127">**Derleme işi** derleme işin durumu ve neden Azure Automation DSC çekme Sunucusu'nda yerleştirilecek düğüm yapılandırmaları (MOF yapılandırma belgeler) izleyebilmeniz için dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="0a503-127">The **Compilation Job** blade is opened so that you can track the compilation job's status, and the node configurations (MOF configuration documents) it caused to be placed on the Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="0a503-128">DSC Yapılandırması Windows PowerShell ile derleme</span><span class="sxs-lookup"><span data-stu-id="0a503-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="0a503-129">Kullanabileceğiniz [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) Windows PowerShell ile derleme başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="0a503-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) to start compiling with Windows PowerShell.</span></span> <span data-ttu-id="0a503-130">Aşağıdaki örnek kod adlı bir DSC yapılandırma derlenmesini başlatır **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="0a503-130">The following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="0a503-131">`Start-AzureRmAutomationDscCompilationJob`durumunu izlemek için kullanabileceğiniz bir derleme iş nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="0a503-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use to track its status.</span></span> <span data-ttu-id="0a503-132">Bu derleme iş nesnesi ile sonra kullanabileceğiniz [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) derleme işi durumunu belirlemek için ve [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) kendi akışlar (çıktı) görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="0a503-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) to determine the status of the compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) to view its streams (output).</span></span> <span data-ttu-id="0a503-133">Aşağıdaki örnek kod derlenmesini başlatır **SampleConfig** yapılandırması tamamlandı ve onun akışları görüntüler kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="0a503-133">The following sample code starts compilation of the **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="0a503-134">Temel parametreleri</span><span class="sxs-lookup"><span data-stu-id="0a503-134">Basic Parameters</span></span>
<span data-ttu-id="0a503-135">DSC yapılandırmaları, parametre türleri ve özellikleriyle birlikte parametresi bildiriminde Azure Otomasyon çalışma kitabı olduğu gibi aynı şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="0a503-135">Parameter declaration in DSC configurations, including parameter types and properties, works the same as in Azure Automation runbooks.</span></span> <span data-ttu-id="0a503-136">Bkz: [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md) runbook parametreleri hakkında daha fazla bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="0a503-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to learn more about runbook parameters.</span></span>

<span data-ttu-id="0a503-137">Aşağıdaki örnek adlı iki parametre kullanır **FeatureName** ve **olmasına**özelliklerinde değerleri belirlemek için **ParametersExample.sample** düğümü derleme sırasında oluşturulan yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="0a503-137">The following example uses two parameters called **FeatureName** and **IsPresent**, to determine the values of properties in the **ParametersExample.sample** node configuration, generated during compilation.</span></span>

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

<span data-ttu-id="0a503-138">Azure Otomasyonu DSC portalında veya Azure PowerShell ile temel parametrelerini kullanmak DSC yapılandırmaları hazırlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0a503-138">You can compile DSC Configurations that use basic parameters in the Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="0a503-139">Portal</span><span class="sxs-lookup"><span data-stu-id="0a503-139">Portal</span></span>

<span data-ttu-id="0a503-140">Portalda, tıkladıktan sonra parametre değerlerini girebilirsiniz **derleme**.</span><span class="sxs-lookup"><span data-stu-id="0a503-140">In the portal, you can enter parameter values after clicking **Compile**.</span></span>

![alternatif metin](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="0a503-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a503-142">PowerShell</span></span>

<span data-ttu-id="0a503-143">PowerShell parametrelerinde gerektiren bir [hashtable](http://technet.microsoft.com/library/hh847780.aspx) burada anahtarının parametre adıyla eşleştiği ve değerin parametre değeri eşittir.</span><span class="sxs-lookup"><span data-stu-id="0a503-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key matches the parameter name, and the value equals the parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="0a503-144">PSCredentials parametre olarak geçirme hakkında daha fazla bilgi için bkz: <a href="#credential-assets"> **kimlik bilgisi varlıkları** </a> aşağıda.</span><span class="sxs-lookup"><span data-stu-id="0a503-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="0a503-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="0a503-145">ConfigurationData</span></span>
<span data-ttu-id="0a503-146">**ConfigurationData** , PowerShell DSC kullanırken hiçbir ortamı belirli yapılandırması yapısal yapılandırmasından ayırmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="0a503-146">**ConfigurationData** allows you to separate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="0a503-147">Bkz: ["Ne" PowerShell DSC "nerede" ayırarak](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) hakkında daha fazla bilgi için **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="0a503-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) to learn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="0a503-148">Kullanabileceğiniz **ConfigurationData** Azure PowerShell kullanarak Azure Otomasyonu DSC, ancak Azure Portalı'ndaki derlerken.</span><span class="sxs-lookup"><span data-stu-id="0a503-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in the Azure portal.</span></span>

<span data-ttu-id="0a503-149">Aşağıdaki örnek DSC yapılandırmasını kullanan **ConfigurationData** aracılığıyla **$ConfigurationData** ve **$AllNodes** anahtar sözcükler.</span><span class="sxs-lookup"><span data-stu-id="0a503-149">The following example DSC configuration uses **ConfigurationData** via the **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="0a503-150">Ayrıca gerekir [ **xWebAdministration** Modülü](https://www.powershellgallery.com/packages/xWebAdministration/) Bu, örneğin:</span><span class="sxs-lookup"><span data-stu-id="0a503-150">You'll also need the [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

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

<span data-ttu-id="0a503-151">Yukarıdaki PowerShell DSC yapılandırması derleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a503-151">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="0a503-152">Aşağıdaki PowerShell iki düğüm yapılandırmaları Azure Automation DSC çekme sunucusuna ekler: **ConfigurationDataSample.MyVM1** ve **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="0a503-152">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

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

## <a name="assets"></a><span data-ttu-id="0a503-153">Varlıklar</span><span class="sxs-lookup"><span data-stu-id="0a503-153">Assets</span></span>

<span data-ttu-id="0a503-154">Varlık başvuruları Azure Otomasyonu DSC yapılandırmaları ve runbook'ları aynıdır.</span><span class="sxs-lookup"><span data-stu-id="0a503-154">Asset references are the same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="0a503-155">Daha fazla bilgi için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="0a503-155">See the following for more information:</span></span>

* [<span data-ttu-id="0a503-156">Sertifikalar</span><span class="sxs-lookup"><span data-stu-id="0a503-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="0a503-157">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="0a503-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="0a503-158">Kimlik Bilgileri</span><span class="sxs-lookup"><span data-stu-id="0a503-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="0a503-159">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="0a503-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="0a503-160">Kimlik bilgisi varlıkları</span><span class="sxs-lookup"><span data-stu-id="0a503-160">Credential Assets</span></span>

<span data-ttu-id="0a503-161">Azure Otomasyonu DSC yapılandırmalarında kullanarak kimlik bilgisi varlıkları başvurabilir sırada **Get-AzureRmAutomationCredential**, kimlik bilgisi varlıkları de geçirilebilir içinde parametreleri aracılığıyla isterseniz.</span><span class="sxs-lookup"><span data-stu-id="0a503-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="0a503-162">Bir yapılandırma parametresi, uzun sürerse **PSCredential** bir Azure Otomasyonu kimlik bilgisi varlığı dize adını bir PSCredential nesnesi yerine bu parametrenin değeri olarak geçirmenize gerek sonra yazın.</span><span class="sxs-lookup"><span data-stu-id="0a503-162">If a configuration takes a parameter of **PSCredential** type, then you need to pass the string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="0a503-163">Arka planda Azure Otomasyonu kimlik bilgisi varlığı bu ada sahip alınabilir ve yapılandırmaya geçirildi.</span><span class="sxs-lookup"><span data-stu-id="0a503-163">Behind the scenes, the Azure Automation credential asset with that name will be retrieved and passed to the configuration.</span></span>

<span data-ttu-id="0a503-164">Kimlik bilgileri tutma düğüm yapılandırmaları (MOF yapılandırma belgeler) güvenli kimlik bilgileri düğüm yapılandırması MOF dosyasındaki şifrelenmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0a503-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting the credentials in the node configuration MOF file.</span></span> <span data-ttu-id="0a503-165">Azure Otomasyonu bunu bir adım daha fazla sürer ve tüm MOF dosyası şifreler.</span><span class="sxs-lookup"><span data-stu-id="0a503-165">Azure Automation takes this one step further and encrypts the entire MOF file.</span></span> <span data-ttu-id="0a503-166">Ancak, şu anda, PowerShell DSC Azure Otomasyonu tüm MOF dosyası neslini sonra şifreleme, PowerShell DSC bilmiyor çünkü için kimlik bilgilerini düz metin olarak düğüm yapılandırması MOF oluşturma sırasında yüzdelik kesebilirsiniz söylemelisiniz derleme işi.</span><span class="sxs-lookup"><span data-stu-id="0a503-166">However, currently you must tell PowerShell DSC it is okay for credentials to be outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting the entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="0a503-167">İçin kimlik bilgilerini düz metin olarak oluşturulan düğüm yapılandırması MOF dosyalarından yüzdelik uygundur PowerShell DSC anlayabilirsiniz kullanarak [ **ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="0a503-167">You can tell PowerShell DSC that it is okay for credentials to be outputted in plain text in the generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="0a503-168">Geçmesi `PSDscAllowPlainTextPassword = $true` aracılığıyla **ConfigurationData** DSC yapılandırması görüntülenir ve kimlik bilgilerini kullanan her düğüm bloğun adı.</span><span class="sxs-lookup"><span data-stu-id="0a503-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in the DSC configuration and uses credentials.</span></span>

<span data-ttu-id="0a503-169">Aşağıdaki örnekte bir Otomasyon kimlik bilgisi varlığı kullanan bir DSC yapılandırmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0a503-169">The following example shows a DSC configuration that uses an Automation credential asset.</span></span>

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

<span data-ttu-id="0a503-170">Yukarıdaki PowerShell DSC yapılandırması derleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a503-170">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="0a503-171">Aşağıdaki PowerShell iki düğüm yapılandırmaları Azure Automation DSC çekme sunucusuna ekler: **CredentialSample.MyVM1** ve **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="0a503-171">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

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

## <a name="importing-node-configurations"></a><span data-ttu-id="0a503-172">Düğüm yapılandırmaları alma</span><span class="sxs-lookup"><span data-stu-id="0a503-172">Importing node configurations</span></span>

<span data-ttu-id="0a503-173">Ayrıca Azure dışında derlediğiniz düğümü configuratons (MOF dosyalarından) içe aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a503-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="0a503-174">Bu bir avantajı, o düğümü confiturations imzalanabilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="0a503-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="0a503-175">İmzalı düğüm yapılandırması düğüme uygulanan yapılandırma yetkili bir kaynaktan geldiğinden emin olduktan DSC aracı tarafından yönetilen bir düğümde yerel olarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="0a503-175">A signed node configuration is verified locally on a managed node by the DSC agent, ensuring that the configuration being applied to the node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="0a503-176">İçeri aktarma kullanabilirsiniz yapılandırmaları Azure Automation hesabınızda oturumu, ancak Azure Otomasyonu desteklememektedir imzalı yapılandırmaları derleme.</span><span class="sxs-lookup"><span data-stu-id="0a503-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="0a503-177">Bir düğüm yapılandırma dosyası Azure Automation'a içeri aktarılacak izin vermek için 1 MB'tan büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0a503-177">A node configuration file must be no larger than 1 MB to allow it to be imported into Azure Automation.</span></span>

<span data-ttu-id="0a503-178">Düğüm yapılandırmaları https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module adresindeki oturum öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a503-178">You can learn how to sign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-the-azure-portal"></a><span data-ttu-id="0a503-179">Azure portalında bir düğüm yapılandırması içe aktarma</span><span class="sxs-lookup"><span data-stu-id="0a503-179">Importing a node configuration in the Azure portal</span></span>

1. <span data-ttu-id="0a503-180">Otomasyon hesabınızdan tıklatın **DSC düğüm yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="0a503-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![DSC düğüm yapılandırmaları](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="0a503-182">İçinde **DSC düğüm yapılandırmaları** dikey penceresinde tıklatın **bir NodeConfiguration eklemek**.</span><span class="sxs-lookup"><span data-stu-id="0a503-182">In the **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="0a503-183">İçinde **alma** dikey penceresinde yanındaki klasör simgesine tıklayın **düğümü yapılandırma dosyası** , yerel bilgisayarınızda bir düğüm yapılandırma dosyası (MOF) göz atmak için metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="0a503-183">In the **Import** blade, click the folder icon next to the **Node Configuration File** textbox to browse for a node configuration file (MOF) on your local computer.</span></span>

    ![Yerel dosya gözatın.](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="0a503-185">Bir ad girin **yapılandırma adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="0a503-185">Enter a name in the **Configuration Name** textbox.</span></span> <span data-ttu-id="0a503-186">Bu ad, düğüm yapılandırması derlenen yapılandırmasının adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="0a503-186">This name must match the name of the configuration from which the node configuration was compiled.</span></span>
5. <span data-ttu-id="0a503-187">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0a503-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="0a503-188">Düğüm yapılandırması PowerShell ile içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="0a503-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="0a503-189">Kullanabileceğiniz [alma AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) düğüm yapılandırması Otomasyon hesabınızda içeri aktarmak için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0a503-189">You can use the [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet to import a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



