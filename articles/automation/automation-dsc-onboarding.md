---
title: "Azure Otomasyonu DSC yönetimine aaaOnboarding makineler | Microsoft Docs"
description: "Azure Otomasyonu DSC ile yönetimi için nasıl toosetup makineleri"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="de744-103">Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler</span><span class="sxs-lookup"><span data-stu-id="de744-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="de744-104">Neden Azure Otomasyonu DSC makinelerle yönetme?</span><span class="sxs-lookup"><span data-stu-id="de744-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="de744-105">Gibi [PowerShell istenen durum Yapılandırması](https://technet.microsoft.com/library/dn249912.aspx), tüm Bulut veya şirket içi veri merkezinde Azure Otomasyonu istenen durum yapılandırması olan DSC düğümleri (fiziksel ve sanal makineler) için basit ancak güçlü, yapılandırma yönetimi hizmeti.</span><span class="sxs-lookup"><span data-stu-id="de744-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="de744-106">Bu ölçeklenebilirliği makineler binlerce arasında hızlı ve kolay bir şekilde bir merkezi, güvenli konumdan sağlar.</span><span class="sxs-lookup"><span data-stu-id="de744-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="de744-107">Her makine bunları bildirim temelli yapılandırmaları ve gösteren raporları görüntüleme Ata uyumluluk istenen toohello durumu, belirtilen kullanıcının, kolayca yerleşik makineler olabilir.</span><span class="sxs-lookup"><span data-stu-id="de744-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance toohello desired state you specified.</span></span> <span data-ttu-id="de744-108">Hello Azure Otomasyonu DSC Yönetimi katmanıdır, tooDSC hangi hello Azure Otomasyonu yönetim katmanı olan tooPowerShell komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="de744-108">hello Azure Automation DSC management layer is tooDSC what hello Azure Automation management layer is tooPowerShell scripting.</span></span> <span data-ttu-id="de744-109">Diğer bir deyişle, hello Azure Otomasyonu yardımcı olacak şekilde PowerShell komut dosyalarını yönetebilir, ayrıca, DSC yapılandırmalarını yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="de744-109">In other words, in hello same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="de744-110">Azure Otomasyonu DSC, daha hello yararları hakkında toolearn bkz [Azure Otomasyonu DSC genel bakış](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de744-110">toolearn more about hello benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="de744-111">Azure Otomasyonu DSC kullanılan toomanage makineler çeşitli olabilir:</span><span class="sxs-lookup"><span data-stu-id="de744-111">Azure Automation DSC can be used toomanage a variety of machines:</span></span>

* <span data-ttu-id="de744-112">Azure sanal makineleri (Klasik)</span><span class="sxs-lookup"><span data-stu-id="de744-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="de744-113">Azure sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="de744-113">Azure virtual machines</span></span>
* <span data-ttu-id="de744-114">Amazon Web Hizmetleri (AWS) sanal makineler</span><span class="sxs-lookup"><span data-stu-id="de744-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="de744-115">Windows fiziksel/sanal makineleri şirket içi veya bulutta Azure/AWS dışında</span><span class="sxs-lookup"><span data-stu-id="de744-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="de744-116">Şirket içi, Azure veya Azure dışında bir bulut Linux fiziksel/sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="de744-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="de744-117">Ayrıca, hazır toomanage makine hello bulut yapılandırmasından olup olmadığı, Azure Automation DSC de yalnızca rapor uç noktası olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="de744-117">In addition, if you are not ready toomanage machine configuration from hello cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="de744-118">Azure Otomasyonu durumda düğüm uyumluluk hello ile ilgili zengin raporlama ayrıntıları görüntüle istenen ve bu DSC şirket içi aracılığıyla tooset (anında iletme) istenen yapılandırma sağlar.</span><span class="sxs-lookup"><span data-stu-id="de744-118">This allows you tooset (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with hello desired state in Azure Automation.</span></span>

<span data-ttu-id="de744-119">Aşağıdaki bölümlerde hello yerleşik nasıl makine tooAzure Automation DSC her tür kullanabilir ana hatlarını vermektedir.</span><span class="sxs-lookup"><span data-stu-id="de744-119">hello following sections outline how you can onboard each type of machine tooAzure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="de744-120">Azure sanal makineleri (Klasik)</span><span class="sxs-lookup"><span data-stu-id="de744-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="de744-121">Azure Otomasyonu DSC'ye hello Azure portal veya PowerShell kullanarak yapılandırma yönetimi için kolayca yerleşik Azure sanal makineleri (Klasik) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de744-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either hello Azure portal, or PowerShell.</span></span> <span data-ttu-id="de744-122">Merhaba başlık altında ve tooremote hello VM uygulamasına sahip bir yönetici olmadan hello Azure VM istenen durum yapılandırması uzantısı hello VM Azure Otomasyonu DSC'ye kaydeder.</span><span class="sxs-lookup"><span data-stu-id="de744-122">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="de744-123">Hello Azure VM istenen durum yapılandırması uzantısı adımları tootrack ilerleme durumunu zaman uyumsuz olarak çalışır veya sorun giderme olduğundan, sağlanan hello [ **sorun giderme Azure sanal makine ekleme** ](#troubleshooting-azure-virtual-machine-onboarding)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="de744-123">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="de744-124">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="de744-124">Azure portal</span></span>

<span data-ttu-id="de744-125">Merhaba, [Azure portal](http://portal.azure.com/), tıklatın **Gözat** -> **sanal makineleri (Klasik)**.</span><span class="sxs-lookup"><span data-stu-id="de744-125">In hello [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="de744-126">Merhaba Windows tooonboard istediğiniz VM seçin.</span><span class="sxs-lookup"><span data-stu-id="de744-126">Select hello Windows VM you want tooonboard.</span></span> <span data-ttu-id="de744-127">Merhaba sanal makinenin Pano dikey penceresinde **tüm ayarları** -> **uzantıları** -> **Ekle**  ->   **Azure Otomasyonu DSC** -> **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="de744-127">On hello virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="de744-128">Merhaba girin [PowerShell DSC Local Configuration Manager değerleri](https://msdn.microsoft.com/powershell/dsc/metaconfig4) kullanım örneği, Otomasyon hesabınızın kayıt anahtarı ve kayıt URL'si ve bir düğüm yapılandırması tooassign toohello VM için isteğe bağlı olarak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="de744-128">Enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="de744-129">toofind hello kayıt URL'si ve anahtar hello Otomasyon hesabı tooonboard hello makine için bkz: Merhaba [ **güvenli kayıt** ](#secure-registration) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="de744-129">toofind hello registration URL and key for hello Automation account tooonboard hello machine to, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="de744-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de744-130">PowerShell</span></span>

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a><span data-ttu-id="de744-131">Azure sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="de744-131">Azure virtual machines</span></span>

<span data-ttu-id="de744-132">Azure Otomasyonu DSC hello Azure portal, Azure Resource Manager şablonları veya PowerShell kullanarak Azure sanal makineleri yapılandırma yönetimi için kolayca yerleşik sağlar.</span><span class="sxs-lookup"><span data-stu-id="de744-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either hello Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="de744-133">Merhaba başlık altında ve tooremote hello VM uygulamasına sahip bir yönetici olmadan hello Azure VM istenen durum yapılandırması uzantısı hello VM Azure Otomasyonu DSC'ye kaydeder.</span><span class="sxs-lookup"><span data-stu-id="de744-133">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="de744-134">Hello Azure VM istenen durum yapılandırması uzantısı adımları tootrack ilerleme durumunu zaman uyumsuz olarak çalışır veya sorun giderme olduğundan, sağlanan hello [ **sorun giderme Azure sanal makine ekleme** ](#troubleshooting-azure-virtual-machine-onboarding)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="de744-134">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="de744-135">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="de744-135">Azure portal</span></span>

<span data-ttu-id="de744-136">Merhaba, [Azure portal](https://portal.azure.com/), toohello Azure Automation hesabını tooonboard sanal makineleri istediğiniz yere gidin.</span><span class="sxs-lookup"><span data-stu-id="de744-136">In hello [Azure portal](https://portal.azure.com/), navigate toohello Azure Automation account where you want tooonboard virtual machines.</span></span> <span data-ttu-id="de744-137">Merhaba Otomasyon hesabı Panoda tıklatın **DSC düğümleri** -> **eklemek Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="de744-137">On hello Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="de744-138">Altında **seçin sanal makineleri tooonboard**daha fazla Azure sanal makineleri tooonboard veya seçin.</span><span class="sxs-lookup"><span data-stu-id="de744-138">Under **Select virtual machines tooonboard**, select one or more Azure virtual machines tooonboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="de744-139">Altında **kayıt verilerini yapılandırma**, hello girin [PowerShell DSC Local Configuration Manager değerleri](https://msdn.microsoft.com/powershell/dsc/metaconfig4) kullanım örneği ve bir düğüm yapılandırması tooassign toohello VM için isteğe bağlı olarak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="de744-139">Under **Configure registration data**, enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="de744-140">Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="de744-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="de744-141">Azure sanal makineler dağıtılabilir ve Azure Resource Manager şablonları aracılığıyla edildi tooAzure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="de744-141">Azure virtual machines can be deployed and onboarded tooAzure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="de744-142">Bkz: [VM DSC uzantısı aracılığıyla ve Azure Otomasyonu DSC yapılandırma](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) bir örnek şablon için bu onboards var olan bir VM tooAzure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="de744-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM tooAzure Automation DSC.</span></span> <span data-ttu-id="de744-143">gerçekleştirilecek toofind hello kayıt anahtarı ve kayıt URL'si bu şablonda giriş olarak hello bkz [ **güvenli kayıt** ](#secure-registration) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="de744-143">toofind hello registration key and registration URL taken as input in this template, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="de744-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de744-144">PowerShell</span></span>

<span data-ttu-id="de744-145">Merhaba [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet hello PowerShell aracılığıyla Azure portalında sanal makinelerinizde kullanılan tooonboard olabilir.</span><span class="sxs-lookup"><span data-stu-id="de744-145">hello [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used tooonboard virtual machines in hello Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="de744-146">Amazon Web Hizmetleri (AWS) sanal makineler</span><span class="sxs-lookup"><span data-stu-id="de744-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="de744-147">Kolayca yerleşik Amazon Web Hizmetleri sanal makineler tarafından hello AWS DSC Araç Seti kullanarak Azure Otomasyonu DSC yapılandırma yönetimi için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de744-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using hello AWS DSC Toolkit.</span></span> <span data-ttu-id="de744-148">Merhaba araç hakkında daha fazla bilgiyi [burada](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="de744-148">You can learn more about hello toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="de744-149">Windows fiziksel/sanal makineleri şirket içi veya bulutta Azure/AWS dışında</span><span class="sxs-lookup"><span data-stu-id="de744-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="de744-150">Şirket içi Windows makinelerini ve Windows Azure olmayan Bulutları (örneğin, Amazon Web Hizmetleri) makinelerinizde de olabilir edildi tooAzure Otomasyonu DSC, giden erişim toohello sahip oldukları sürece birkaç basit adımda üzerinden internet:</span><span class="sxs-lookup"><span data-stu-id="de744-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="de744-151">Emin hello en son sürümünü olun [WMF 5](http://aka.ms/wmf5latest) yüklü hello makinelerde tooonboard tooAzure Automation DSC istiyor.</span><span class="sxs-lookup"><span data-stu-id="de744-151">Make sure hello latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="de744-152">Merhaba bölümündeki yönergeleri izleyin [ **oluşturma DSC metaconfigurations** ](#generating-dsc-metaconfigurations) toogenerate DSC metaconfigurations hello içeren klasörü gerekli.</span><span class="sxs-lookup"><span data-stu-id="de744-152">Follow hello directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="de744-153">Uzaktan hello PowerShell DSC meta yapılandırmasını toohello makineler tooonboard istediğiniz uygulayın.</span><span class="sxs-lookup"><span data-stu-id="de744-153">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard.</span></span> <span data-ttu-id="de744-154">**Merhaba makinesinin bu komutu çalıştırmak, hello en son sürümünü olmalıdır [WMF 5](http://aka.ms/wmf5latest) yüklü**:</span><span class="sxs-lookup"><span data-stu-id="de744-154">**hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="de744-155">Merhaba PowerShell DSC metaconfigurations uzaktan uygulanamıyor varsa, 2. adımda her makine tooonboard üzerine hello metaconfigurations klasörüne kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="de744-155">If you cannot apply hello PowerShell DSC metaconfigurations remotely, copy hello metaconfigurations folder from step 2 onto each machine tooonboard.</span></span> <span data-ttu-id="de744-156">' I çağırın **kümesi DscLocalConfigurationManager** her makine tooonboard yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="de744-156">Then call **Set-DscLocalConfigurationManager** locally on each machine tooonboard.</span></span>
5. <span data-ttu-id="de744-157">Hello Azure portal veya cmdlet'ler, Azure Otomasyon hesabınızda hello makineler tooonboard şimdi gösterisini DSC düğümleri olarak kayıtlı onay kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="de744-157">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="de744-158">Şirket içi, Azure veya Azure dışında bir bulut Linux fiziksel/sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="de744-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="de744-159">Şirket içi Linux makineler için Azure, Linux makinelerde ve Linux Azure olmayan bulut makinelerinizde de olabilir edildi tooAzure Otomasyonu DSC, giden erişim toohello sahip oldukları sürece birkaç basit adımda üzerinden internet:</span><span class="sxs-lookup"><span data-stu-id="de744-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="de744-160">Emin hello en son sürümünü olun [PowerShell istenen durum yapılandırması Linux için](https://github.com/Microsoft/PowerShell-DSC-for-Linux) yüklü hello makinelerde tooonboard tooAzure Automation DSC istiyor.</span><span class="sxs-lookup"><span data-stu-id="de744-160">Make sure hello latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="de744-161">Merhaba, [PowerShell DSC Local Configuration Manager varsayılanları](https://msdn.microsoft.com/powershell/dsc/metaconfig4) , kullanım büyük küçük harf duyarlı ve tooonboard makineleri gibi istediğiniz, bunlar **her ikisi de** isteneceğini ve tooAzure Automation DSC Rapor:</span><span class="sxs-lookup"><span data-stu-id="de744-161">If hello [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want tooonboard machines such that they **both** pull from and report tooAzure Automation DSC:</span></span>

   + <span data-ttu-id="de744-162">Her Linux makine tooonboard tooAzure üzerinde Otomasyonu DSC, PowerShell DSC Local Configuration Manager varsayılan olarak hello kullanarak Register.py tooonboard kullanın:</span><span class="sxs-lookup"><span data-stu-id="de744-162">On each Linux machine tooonboard tooAzure Automation DSC, use Register.py tooonboard using hello PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="de744-163">toofind hello kayıt anahtarı ve kayıt Automation hesabınız için URL'i hello [ **güvenli kayıt** ](#secure-registration) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="de744-163">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="de744-164">Merhaba, PowerShell DSC Local Configuration Manager varsayılan olarak **yapmak** **değil** tooonboard makineleri bunlar yalnızca tooAzure Automation DSC rapor, ancak değil çekme şekilde istediğiniz veya kullanım örneği eşleşmesi yapılandırma veya PowerShell modülleri, adım 3-6 izleyin.</span><span class="sxs-lookup"><span data-stu-id="de744-164">If hello PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want tooonboard machines such that they only report tooAzure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="de744-165">Aksi takdirde, doğrudan toostep 6 devam edin.</span><span class="sxs-lookup"><span data-stu-id="de744-165">Otherwise, proceed directly toostep 6.</span></span>

3. <span data-ttu-id="de744-166">Merhaba hello içindeki yönergeleri izleyin [ **oluşturma DSC metaconfigurations** ](#generating-dsc-metaconfigurations) gerekli hello DSC metaconfigurations içeren klasörü toogenerate bölümünde.</span><span class="sxs-lookup"><span data-stu-id="de744-166">Follow hello directions in hello [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="de744-167">Uzaktan hello PowerShell DSC meta yapılandırmasını toohello makineler tooonboard istediğiniz Uygula:</span><span class="sxs-lookup"><span data-stu-id="de744-167">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="de744-168">Merhaba makinesinin bu komutu çalıştırmak, hello en son sürümünü olmalıdır [WMF 5](http://aka.ms/wmf5latest) yüklü.</span><span class="sxs-lookup"><span data-stu-id="de744-168">hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="de744-169">Merhaba PowerShell DSC metaconfigurations her Linux makine tooonboard için uzaktan uygulayamazsınız, hello meta yapılandırmasını karşılık gelen toothat makine hello Linux makine üzerine 5. adımda hello klasörünü kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="de744-169">If you cannot apply hello PowerShell DSC metaconfigurations remotely, for each Linux machine tooonboard, copy hello metaconfiguration corresponding toothat machine from hello folder in step 5 onto hello Linux machine.</span></span> <span data-ttu-id="de744-170">' I çağırın `SetDscLocalConfigurationManager.py` yerel olarak tooonboard tooAzure Automation DSC istediğiniz her Linux makinesinde:</span><span class="sxs-lookup"><span data-stu-id="de744-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want tooonboard tooAzure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. <span data-ttu-id="de744-171">Hello Azure portal veya cmdlet'ler, Azure Otomasyon hesabınızda hello makineler tooonboard şimdi gösterisini DSC düğümleri olarak kayıtlı onay kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="de744-171">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="de744-172">DSC metaconfigurations oluşturma</span><span class="sxs-lookup"><span data-stu-id="de744-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="de744-173">toogenerically tooAzure Otomasyonu DSC, herhangi bir makine yerleşik bir [DSC meta yapılandırmasını](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) olabilir uygulanan, hello DSC Aracısı hello makine toopull bildirir ve/veya tooAzure Automation DSC rapor, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="de744-173">toogenerically onboard any machine tooAzure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells hello DSC agent on hello machine toopull from and/or report tooAzure Automation DSC.</span></span> <span data-ttu-id="de744-174">Azure Otomasyonu DSC DSC metaconfigurations bir PowerShell DSC yapılandırması ya da hello Azure Automation PowerShell cmdlet'lerini kullanarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="de744-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or hello Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="de744-175">DSC metaconfigurations hello gereken gizli tooonboard makine tooan Otomasyon hesabı Yönetim için içerir.</span><span class="sxs-lookup"><span data-stu-id="de744-175">DSC metaconfigurations contain hello secrets needed tooonboard a machine tooan Automation account for management.</span></span> <span data-ttu-id="de744-176">Oluşturduğunuz tüm DSC metaconfigurations korumak veya kullandıktan sonra silin emin tooproperly olun.</span><span class="sxs-lookup"><span data-stu-id="de744-176">Make sure tooproperly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="de744-177">DSC Yapılandırması'nı kullanarak</span><span class="sxs-lookup"><span data-stu-id="de744-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="de744-178">Yerel ortamınızdaki bir makinede Hello PowerShell ISE'yi yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="de744-178">Open hello PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="de744-179">Merhaba makine hello en son sürümünü olmalıdır [WMF 5](http://aka.ms/wmf5latest) yüklü.</span><span class="sxs-lookup"><span data-stu-id="de744-179">hello machine must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="de744-180">Komut dosyası yerel olarak aşağıdaki hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="de744-180">Copy hello following script locally.</span></span> <span data-ttu-id="de744-181">Bu komut dosyası metaconfigurations ve komut tookick hello meta yapılandırmasını oluşturma devre dışı oluşturmak için PowerShell DSC yapılandırması içerir.</span><span class="sxs-lookup"><span data-stu-id="de744-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command tookick off hello metaconfiguration creation.</span></span>

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="de744-182">Merhaba kayıt anahtarı ve URL, Automation hesabı, yanı sıra hello makineler tooonboard hello adlarını doldurun.</span><span class="sxs-lookup"><span data-stu-id="de744-182">Fill in hello registration key and URL for your Automation account, as well as hello names of hello machines tooonboard.</span></span> <span data-ttu-id="de744-183">Diğer tüm parametreler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="de744-183">All other parameters are optional.</span></span> <span data-ttu-id="de744-184">toofind hello kayıt anahtarı ve kayıt Automation hesabınız için URL'i hello [ **güvenli kayıt** ](#secure-registration) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="de744-184">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="de744-185">Merhaba makineler tooreport DSC durum bilgileri tooAzure Automation DSC istiyor, ancak yapılandırma veya PowerShell modülleri çekme değil, hello ayarlamak **sadece rapor** parametresi tootrue.</span><span class="sxs-lookup"><span data-stu-id="de744-185">If you want hello machines tooreport DSC status information tooAzure Automation DSC, but not pull configuration or PowerShell modules, set hello **ReportOnly** parameter tootrue.</span></span>
5. <span data-ttu-id="de744-186">Merhaba komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="de744-186">Run hello script.</span></span> <span data-ttu-id="de744-187">Adlı bir klasör şimdi olmalıdır **DscMetaConfigs** hello PowerShell DSC metaconfigurations hello makineler tooonboard (Yönetici) olarak için çalışma dizininizi içeren:</span><span class="sxs-lookup"><span data-stu-id="de744-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a><span data-ttu-id="de744-188">Hello Azure Automation cmdlet'leri kullanma</span><span class="sxs-lookup"><span data-stu-id="de744-188">Using hello Azure Automation cmdlets</span></span>

<span data-ttu-id="de744-189">Kullanım örneği Hello PowerShell DSC Local Configuration Manager Varsayılanları eşlemek ve bunlar isteneceğini hem tooAzure Automation DSC rapor şekilde tooonboard makineler istiyorsanız hello Azure Automation cmdlet'leri hello DSC oluşturmanın basitleştirilmiş bir yöntem sağlar. gerekli metaconfigurations:</span><span class="sxs-lookup"><span data-stu-id="de744-189">If hello PowerShell DSC Local Configuration Manager defaults match your use case, and you want tooonboard machines such that they both pull from and report tooAzure Automation DSC, hello Azure Automation cmdlets provide a simplified method of generating hello DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="de744-190">Yerel ortamınızdaki bir makinede Hello PowerShell konsolunu veya PowerShell ISE'yi yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="de744-190">Open hello PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="de744-191">TooAzure Kaynak Yöneticisi'ni kullanarak bağlanmak **Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="de744-191">Connect tooAzure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="de744-192">Merhaba Otomasyon gelen tooonboard istediğiniz hello makineler tooonboard düğümleri istediğiniz toowhich hesabı için hello PowerShell DSC metaconfigurations yükleyin:</span><span class="sxs-lookup"><span data-stu-id="de744-192">Download hello PowerShell DSC metaconfigurations for hello machines you want tooonboard from hello Automation account toowhich you want tooonboard nodes:</span></span>

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="de744-193">Adlı bir klasör şimdi olmalıdır ***DscMetaConfigs***, hello PowerShell DSC metaconfigurations hello makineler tooonboard (Yönetici) olarak için içeren:</span><span class="sxs-lookup"><span data-stu-id="de744-193">You should now have a folder called ***DscMetaConfigs***, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="de744-194">Güvenli kayıt</span><span class="sxs-lookup"><span data-stu-id="de744-194">Secure registration</span></span>

<span data-ttu-id="de744-195">Makineler güvenli bir şekilde yerleşik tooan (Azure Otomasyonu DSC dahil) bir DSC düğümü tooauthenticate tooa PowerShell V2 DSC çekme veya Raporlama sunucusu verir hello WMF 5 DSC kaydı protokolü aracılığıyla Azure Automation hesabını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de744-195">Machines can securely onboard tooan Azure Automation account through hello WMF 5 DSC registration protocol, which allows a DSC node tooauthenticate tooa PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="de744-196">Merhaba düğümü kaydeder toohello sunucuda bir **kayıt URL'si**, kimlik doğrulama kullanarak bir **kayıt anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="de744-196">hello node registers toohello server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="de744-197">Kayıt sırasında hello DSC düğümü ve DSC çekme/raporlama sunucusu kimlik doğrulaması toohello sunucu sonrası kaydı için bu düğümü toouse için benzersiz bir sertifika anlaşmaları.</span><span class="sxs-lookup"><span data-stu-id="de744-197">During registration, hello DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node toouse for authentication toohello server post-registration.</span></span> <span data-ttu-id="de744-198">Bu işlem, bir başka bir düğüm bir gibi tehlikeye kimliğine bürünmek ve kötü amaçlı olarak davranmakta edildi düğümleri engeller.</span><span class="sxs-lookup"><span data-stu-id="de744-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="de744-199">Kayıt sonra hello kayıt anahtarını yeniden kimlik doğrulaması için kullanılmaz ve hello düğümden silinir.</span><span class="sxs-lookup"><span data-stu-id="de744-199">After registration, hello Registration key is not used for authentication again, and is deleted from hello node.</span></span>

<span data-ttu-id="de744-200">Merhaba DSC kaydı hello protokolünden için gereken hello bilgiler alabilirsiniz **anahtarları Yönet** dikey penceresinde hello Azure Önizleme portalı.</span><span class="sxs-lookup"><span data-stu-id="de744-200">You can get hello information required for hello DSC registration protocol from hello **Manage Keys** blade in hello Azure preview portal.</span></span> <span data-ttu-id="de744-201">Bu dikey penceresinde hello hello anahtar simgesine tıklayarak açın **Essentials** paneli hello Otomasyon hesabı için.</span><span class="sxs-lookup"><span data-stu-id="de744-201">Open this blade by clicking hello key icon on hello **Essentials** panel for hello Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="de744-202">Kayıt URL'si hello URL hello anahtarları Yönet dikey penceresinde bir alandır.</span><span class="sxs-lookup"><span data-stu-id="de744-202">Registration URL is hello URL field in hello Manage Keys blade.</span></span>
* <span data-ttu-id="de744-203">Kayıt anahtarı hello anahtarları Yönet dikey penceresinde hello birincil erişim tuşunu veya ikincil erişim anahtarını değil.</span><span class="sxs-lookup"><span data-stu-id="de744-203">Registration key is hello Primary Access Key or Secondary Access Key in hello Manage Keys blade.</span></span> <span data-ttu-id="de744-204">Her iki anahtar kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="de744-204">Either key can be used.</span></span>

<span data-ttu-id="de744-205">Ek güvenlik için herhangi bir anda bir Otomasyon hesabı hello birincil ve ikincil erişim anahtarlarını üretilebilir (Merhaba üzerinde **anahtarları Yönet** dikey) önceki anahtar kullanılarak tooprevent gelecekteki düğümü kayıtlar.</span><span class="sxs-lookup"><span data-stu-id="de744-205">For added security, hello primary and secondary access keys of an Automation account can be regenerated at any time (on hello **Manage Keys** blade) tooprevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="de744-206">Sorun giderme Azure sanal makine ekleme</span><span class="sxs-lookup"><span data-stu-id="de744-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="de744-207">Azure Otomasyonu DSC, yapılandırma yönetimi için Azure Windows Vm'lerini kolayca eklemeyi olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="de744-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="de744-208">Merhaba başlık altında hello Azure VM istenen durum yapılandırması uzantısı kullanılan tooregister hello Azure Otomasyonu DSC VM ' dir.</span><span class="sxs-lookup"><span data-stu-id="de744-208">Under hello hood, hello Azure VM Desired State Configuration extension is used tooregister hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="de744-209">Hello Azure VM istenen durum yapılandırması uzantısı zaman uyumsuz olarak çalışır olduğundan, ilerleme durumunu izleme ve sorun giderme yürütülmesinin önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="de744-209">Since hello Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="de744-210">Bir Azure Windows VM tooAzure hello Azure VM istenen durum yapılandırması uzantısını kullanır Automation DSC tooan saat hello düğümü tooshow için ayarlama Azure Otomasyonu'nda kayıtlı olarak ele geçirebilir ekleme herhangi bir yöntemini.</span><span class="sxs-lookup"><span data-stu-id="de744-210">Any method of onboarding an Azure Windows VM tooAzure Automation DSC that uses hello Azure VM Desired State Configuration extension could take up tooan hour for hello node tooshow up as registered in Azure Automation.</span></span> <span data-ttu-id="de744-211">Toohello yüklemesinde Windows Management Framework 5.0 hello VM gerekli tooonboard hello VM tooAzure Automation DSC olduğu hello Azure VM DSC uzantısı tarafından son budur.</span><span class="sxs-lookup"><span data-stu-id="de744-211">This is due toohello installation of Windows Management Framework 5.0 on hello VM by hello Azure VM DSC extension, which is required tooonboard hello VM tooAzure Automation DSC.</span></span>

<span data-ttu-id="de744-212">hello Azure VM istenen durum yapılandırması uzantısı'hello Azure Portalı'nda tootroubleshoot veya Görünüm hello durumunu gidin toohello edildi olan VM tıklatın ardından -> **tüm ayarları** -> **uzantıları**   ->  **DSC**.</span><span class="sxs-lookup"><span data-stu-id="de744-212">tootroubleshoot or view hello status of hello Azure VM Desired State Configuration extension, in hello Azure portal navigate toohello VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="de744-213">Daha fazla ayrıntı için tıklattığınız **ayrıntılı durumunu görüntüleme**.</span><span class="sxs-lookup"><span data-stu-id="de744-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="de744-214">Sertifika geçerlilik süresi ve saklanması</span><span class="sxs-lookup"><span data-stu-id="de744-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="de744-215">Bir Azure Otomasyonu DSC DSC düğüm olarak bir makine kaydolduktan sonra pek çok neden tooreregister hello bu düğümünde gelecekteki ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="de744-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need tooreregister that node in hello future:</span></span>

* <span data-ttu-id="de744-216">Kaydolduktan sonra her düğüme benzersiz bir sertifikası bir yıl sonra süresi dolar kimlik doğrulaması için otomatik olarak görüşür.</span><span class="sxs-lookup"><span data-stu-id="de744-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="de744-217">Şu anda, bir yılın zamanından sonra tooreregister hello düğümleri gerekiyor süre sonu yaklaştığı zaman hello PowerShell DSC kaydı Protokolü otomatik olarak sertifikalarını yenileyemiyor.</span><span class="sxs-lookup"><span data-stu-id="de744-217">Currently, hello PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need tooreregister hello nodes after a year's time.</span></span> <span data-ttu-id="de744-218">Yeniden önce her düğüm Windows Management Framework 5.0 RTM çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="de744-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="de744-219">Bir düğümün kimlik doğrulama sertifikasının süresi dolar ve hello düğümü değil yeniden kaydetme, hello düğümü Azure Automation oluşturulamıyor toocommunicate olacak ve 'Unresponsive.' işaretlenir</span><span class="sxs-lookup"><span data-stu-id="de744-219">If a node's authentication certificate expires, and hello node is not reregistered, hello node will be unable toocommunicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="de744-220">90 gün saklanması gerçekleştirilen veya küçük hello sertifika sona erme saati veya hello sertifika sona erme saati sonra herhangi bir noktada oluşturulan ve kullanılan yeni bir sertifika içinde neden olur.</span><span class="sxs-lookup"><span data-stu-id="de744-220">Reregistration performed 90 days or less from hello certificate expiration time, or at any point after hello certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="de744-221">toochange herhangi [PowerShell DSC Local Configuration Manager değerleri](https://msdn.microsoft.com/powershell/dsc/metaconfig4) ConfigurationMode gibi hello düğümünün ilk kaydı sırasında kümesi.</span><span class="sxs-lookup"><span data-stu-id="de744-221">toochange any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of hello node, such as ConfigurationMode.</span></span> <span data-ttu-id="de744-222">Şu anda bu DSC Aracısı değerleri yalnızca yeniden kayıt işlemi değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="de744-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="de744-223">Merhaba tek özel durum hello düğüm toohello düğümü atanan yapılandırması kullanılır--bu doğrudan Azure Otomasyonu DSC değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="de744-223">hello one exception is hello Node Configuration assigned toohello node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="de744-224">Yeniden kayıt işlemi hello düğümü başlangıçta hello ekleme yöntemlerden birini kullanarak kaydettiğiniz aynı şekilde bu belgede açıklanan hello gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="de744-224">Reregistration can be performed in hello same way you registered hello node initially, using any of hello onboarding methods described in this document.</span></span> <span data-ttu-id="de744-225">Azure Otomasyonu DSC düğüm toounregister yeniden önce gerekmez.</span><span class="sxs-lookup"><span data-stu-id="de744-225">You do not need toounregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="de744-226">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="de744-226">Related Articles</span></span>

* [<span data-ttu-id="de744-227">Azure Otomasyonu DSC genel bakış</span><span class="sxs-lookup"><span data-stu-id="de744-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="de744-228">Azure Otomasyonu DSC cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="de744-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="de744-229">Azure Otomasyonu DSC fiyatlandırması</span><span class="sxs-lookup"><span data-stu-id="de744-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
