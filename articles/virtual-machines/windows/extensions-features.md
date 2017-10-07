---
title: "Windows Azure için aaaVirtual makine uzantıları ve özellikleri | Microsoft Docs"
description: "Hangi uzantıları ne bunlar sağlayın veya geliştirmek tarafından gruplandırılmış Azure sanal makineler için kullanılabilir olduğunu öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="b4ef0-103">Sanal makine uzantıları ve özellikleri Windows için</span><span class="sxs-lookup"><span data-stu-id="b4ef0-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="b4ef0-104">Azure sanal makine uzantıları Azure sanal makinelerde dağıtım sonrası yapılandırma ve Otomasyon görevlerini sağlayan küçük uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="b4ef0-105">Örneğin, bir sanal makineye yazılım yükleme, virüsten koruma veya Docker yapılandırma gerektiriyorsa, VM uzantısı için kullanılan toocomplete bu görevleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="b4ef0-106">Azure VM uzantıları ve Azure portal hello hello Azure CLI, PowerShell, Azure Resource Manager şablonları kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-106">Azure VM extensions can be run by using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="b4ef0-107">Uzantıları ile yeni bir sanal makine dağıtımı paketlenebilir veya varolan bir sistemle bağlantılı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="b4ef0-108">Bu belge, sanal makine uzantıları, sanal makine uzantıları ve Kılavuzu nasıl toodetect, yönetme ve sanal makine uzantıları kaldırma üzerinde kullanma önkoşulları genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how toodetect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="b4ef0-109">Birçok VM uzantıları bulunduğundan, bu belgede genelleştirilmiş bilgiler sağlanmaktadır her potansiyel olarak benzersiz bir yapılandırmaya sahip.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="b4ef0-110">Uzantı özel ayrıntıları her belge belirli toohello tek tek uzantısı'nda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="b4ef0-111">Kullanım örnekleri ve örnekler</span><span class="sxs-lookup"><span data-stu-id="b4ef0-111">Use cases and samples</span></span>

<span data-ttu-id="b4ef0-112">Birçok farklı Azure VM uzantıları vardır, her biri belirli bir kullanım örneği.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="b4ef0-113">Bazı örnek kullanım örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b4ef0-113">Some example use cases are:</span></span>

- <span data-ttu-id="b4ef0-114">PowerShell istenen durum yapılandırması tooa sanal makine için Windows hello DSC uzantısı kullanılarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-114">Apply PowerShell Desired State configurations tooa virtual machine by using hello DSC extension for Windows.</span></span> <span data-ttu-id="b4ef0-115">Daha fazla bilgi için bkz: [Azure istenen durum yapılandırması uzantısı](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b4ef0-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="b4ef0-116">Sanal makine hello Microsoft İzleme Aracısı VM uzantısı kullanarak izlemeyi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-116">Configure virtual machine monitoring by using hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="b4ef0-117">Daha fazla bilgi için bkz: [bağlanmak Azure sanal makineleri tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b4ef0-117">For more information, see [Connect Azure virtual machines tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="b4ef0-118">Azure altyapınızın hello Datadog uzantısı ile izlemeyi yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="b4ef0-119">Daha fazla bilgi için bkz: Merhaba [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="b4ef0-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="b4ef0-120">Bir Azure sanal makinesi Chef kullanarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="b4ef0-121">Daha fazla bilgi için bkz: [otomatikleştirme Azure sanal makine dağıtımı Chef ile](chef-automation.md).</span><span class="sxs-lookup"><span data-stu-id="b4ef0-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="b4ef0-122">Ayrıca tooprocess özgü uzantılar, özel betik uzantısı hem Windows hem de Linux sanal makineler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="b4ef0-123">Merhaba özel betik uzantısı Windows için bir sanal makine üzerinde çalışan bir PowerShell komut dosyası toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-123">hello Custom Script extension for Windows allows any PowerShell script toobe run on a virtual machine.</span></span> <span data-ttu-id="b4ef0-124">Yerel hangi Azure araçlar sağlayabilir ötesinde yapılandırma gerektiren Azure dağıtımları tasarlarken kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="b4ef0-125">Daha fazla bilgi için bkz: [Windows VM özel betik uzantısı](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="b4ef0-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b4ef0-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b4ef0-126">Prerequisites</span></span>

<span data-ttu-id="b4ef0-127">Her sanal makine uzantısı önkoşulları kendi kümesine sahip.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="b4ef0-128">Örneği için bir önkoşul desteklenen Linux dağıtım hello Docker VM uzantısı vardır.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="b4ef0-129">Tek tek uzantıların gereksinimlerini hello uzantıya özgü belgelerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="b4ef0-130">Azure VM aracısı</span><span class="sxs-lookup"><span data-stu-id="b4ef0-130">Azure VM agent</span></span>
<span data-ttu-id="b4ef0-131">Hello Azure VM Aracısı bir Azure sanal makinesi ve hello Azure yapı denetleyicisi arasındaki etkileşimi yönetir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-131">hello Azure VM agent manages interaction between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="b4ef0-132">Merhaba VM Aracısı dağıtma ve yönetme Azure sanal makineler, çalışan VM uzantıları dahil olmak üzere birçok işlevsel görünüşlere için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="b4ef0-133">Hello Azure VM Aracısı Azure Marketi görüntülerinde önceden yüklenmiş ve desteklenen işletim sistemlerine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="b4ef0-134">Desteklenen işletim sistemleri ve yükleme yönergeleri hakkında daha fazla bilgi için bkz: [Azure sanal makine Aracısı](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b4ef0-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="b4ef0-135">VM uzantıları Bul</span><span class="sxs-lookup"><span data-stu-id="b4ef0-135">Discover VM extensions</span></span>
<span data-ttu-id="b4ef0-136">Birçok farklı VM uzantıları, Azure sanal makineler ile kullanmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="b4ef0-137">tam bir listesi, toosee komutu hello Azure Resource Manager PowerShell modülü ile aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-137">toosee a complete list, run hello following command with hello Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="b4ef0-138">Bu komutu çalıştırdığınızda toospecify istenen hello konumu emin olun.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-138">Make sure toospecify hello desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="b4ef0-139">VM uzantıları çalıştırın</span><span class="sxs-lookup"><span data-stu-id="b4ef0-139">Run VM extensions</span></span>

<span data-ttu-id="b4ef0-140">Azure sanal makine uzantıları toomake yapılandırma değişiklikleri gerekir ya da bağlantı zaten dağıtılmış bir VM'de kurtarmak gerektiğinde faydalı olan mevcut sanal makinelerde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="b4ef0-141">VM uzantıları, Azure Resource Manager şablonu dağıtımlarında da gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="b4ef0-142">Resource Manager şablonları ile uzantıları kullanarak dağıtılır ve dağıtım sonrası araya hello gerek kalmadan yapılandırılmış Azure sanal makineleri toobe etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines toobe deployed and configured without hello need for post-deployment intervention.</span></span>

<span data-ttu-id="b4ef0-143">yöntemler aşağıdaki hello kullanılan toorun uzantı var olan bir sanal makineye karşı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-143">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="b4ef0-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4ef0-144">PowerShell</span></span>

<span data-ttu-id="b4ef0-145">Birkaç PowerShell komutları tek tek uzantıların çalıştırmak için mevcut.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="b4ef0-146">bir liste toosee hello aşağıdaki PowerShell komutlarını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-146">toosee a list, run hello following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="b4ef0-147">Bu çıktı benzer toohello aşağıdakileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="b4ef0-147">This provides output similar toohello following:</span></span>

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

<span data-ttu-id="b4ef0-148">Merhaba aşağıdaki örnek hello özel betik uzantısı toodownload bir komut dosyası hello hedef sanal makine üzerine GitHub deposunu kullanır ve hello betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-148">hello following example uses hello Custom Script extension toodownload a script from a GitHub repository onto hello target virtual machine and then run hello script.</span></span> <span data-ttu-id="b4ef0-149">Merhaba özel betik uzantısı ile ilgili daha fazla bilgi için bkz: [özel betik uzantısı genel bakış](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="b4ef0-149">For more information on hello Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="b4ef0-150">Bu örnekte, hello VM erişim uzantısı kullanılan tooreset hello yönetimsel bir Windows sanal makinenin paroladır.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-150">In this example, hello VM Access extension is used tooreset hello administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="b4ef0-151">Merhaba VM erişim uzantısı ile ilgili daha fazla bilgi için bkz: [Windows VM Uzak Masaüstü'nü Sıfırla Hizmeti'nde](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="b4ef0-151">For more information on hello VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="b4ef0-152">Merhaba `Set-AzureRmVMExtension` komutu kullanılan toostart tüm VM uzantısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-152">hello `Set-AzureRmVMExtension` command can be used toostart any VM extension.</span></span> <span data-ttu-id="b4ef0-153">Daha fazla bilgi için bkz: Merhaba [kümesi AzureRmVMExtension başvuru](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4ef0-153">For more information, see hello [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="b4ef0-154">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="b4ef0-154">Azure portal</span></span>

<span data-ttu-id="b4ef0-155">VM uzantısı hello Azure portal aracılığıyla uygulanan tooan varolan sanal makine olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-155">A VM extension can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="b4ef0-156">toodo, bu nedenle, hello sanal makine seçin toouse istiyorsanız, seçin **uzantıları**, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-156">toodo so, select hello virtual machine you want toouse, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="b4ef0-157">Bu, kullanılabilir uzantıları listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-157">This provides a list of available extensions.</span></span> <span data-ttu-id="b4ef0-158">Merhaba istediğiniz ve hello hello Sihirbazı'ndaki adımları seçin.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-158">Select hello one you want and follow hello steps in hello wizard.</span></span>

<span data-ttu-id="b4ef0-159">Merhaba aşağıdaki görüntüde hello hello Azure portal Microsoft Antimalware uzantı hello yüklemesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-159">hello following image shows hello installation of hello Microsoft Antimalware extension from hello Azure portal.</span></span>

![Kötü amaçlı yazılımdan koruma uzantısını yükleyin](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="b4ef0-161">Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="b4ef0-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="b4ef0-162">VM uzantıları eklenen tooan Azure Resource Manager şablonu olabilir ve hello şablon hello dağıtımı ile yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-162">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="b4ef0-163">Bir şablonla uzantıları tam olarak yapılandırılmış Azure dağıtımları oluşturmak için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="b4ef0-164">Örneğin, aşağıdaki JSON yük dengeli sanal makineler ve Azure SQL veritabanını kümesi dağıtır ve ardından her VM .NET Core uygulama yükleyen bir Resource Manager şablonu alınırlar hello.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-164">For example, hello following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="b4ef0-165">Merhaba VM uzantısı hello yazılım yüklemesini mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-165">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="b4ef0-166">Daha fazla bilgi için bkz: Merhaba [tam Resource Manager şablonu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="b4ef0-166">For more information, see hello [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="b4ef0-167">Daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma Windows VM uzantıları ile](template-description.md#extensions).</span><span class="sxs-lookup"><span data-stu-id="b4ef0-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="b4ef0-168">VM uzantısı verileri güvenli</span><span class="sxs-lookup"><span data-stu-id="b4ef0-168">Secure VM extension data</span></span>

<span data-ttu-id="b4ef0-169">VM uzantısı çalıştırırken kimlik bilgilerini, depolama hesabı adları ve depolama hesabı erişim anahtarlarını gibi hassas bilgileri gerekli tooinclude olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-169">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="b4ef0-170">Birçok VM uzantıları verileri şifreler ve yalnızca hello hedef sanal makine içinde şifresini çözer korumalı bir yapılandırmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="b4ef0-171">Her bir uzantı uzantıya özgü belgelerinde ayrıntılı bir belirli korumalı yapılandırma şeması vardır.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="b4ef0-172">Aşağıdaki örneğine hello için Windows hello özel betik uzantısı örneğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-172">hello following example shows an instance of hello Custom Script extension for Windows.</span></span> <span data-ttu-id="b4ef0-173">Bu hello komutu tooexecute kimlik bilgileri kümesi içerir dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-173">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="b4ef0-174">Bu örnekte, hello komutu tooexecute şifrelenmez.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-174">In this example, hello command tooexecute will not be encrypted.</span></span>


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="b4ef0-175">Merhaba taşıyarak Hello yürütme dize güvenli **komutu tooexecute** özelliği toohello **korumalı** yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-175">Secure hello execution string by moving hello **command tooexecute** property toohello **protected** configuration.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="b4ef0-176">VM uzantıları sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b4ef0-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="b4ef0-177">Her VM uzantısı özel sorun giderme adımları olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="b4ef0-178">Örneğin, hello özel betik uzantısı kullanırken, komut dosyası yürütme ayrıntılarını yerel olarak hello uzantısı çalıştırıldığı hello sanal makine üzerinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-178">For instance, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="b4ef0-179">Uzantı özel sorun giderme işlemleri uzantıya özgü belgelerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="b4ef0-180">Aşağıdaki sorun giderme adımları hello tooall sanal makine uzantıları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-180">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="b4ef0-181">Uzantı durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="b4ef0-181">View extension status</span></span>

<span data-ttu-id="b4ef0-182">Bir sanal makine uzantısı bir sanal makine çalıştırdıktan sonra aşağıdaki PowerShell komut tooreturn uzantı durumunu hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-182">After a virtual machine extension has been run against a virtual machine, use hello following PowerShell command tooreturn extension status.</span></span> <span data-ttu-id="b4ef0-183">Örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="b4ef0-184">Merhaba `Name` parametresi toohello uzantısı yürütme sırasında verilen hello adı alır.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-184">hello `Name` parameter takes hello name given toohello extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="b4ef0-185">Merhaba çıktı hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="b4ef0-185">hello output looks like hello following:</span></span>

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

<span data-ttu-id="b4ef0-186">Uzantı yürütme durumu da hello Azure portalında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-186">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="b4ef0-187">tooview hello durumu select hello sanal makine, bir uzantı seçin **uzantıları**, ve hello istenen uzantı seçin.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-187">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="b4ef0-188">VM uzantıları yeniden çalıştırın</span><span class="sxs-lookup"><span data-stu-id="b4ef0-188">Rerun VM extensions</span></span>

<span data-ttu-id="b4ef0-189">Bir sanal makine uzantısı toobe gereken durumlar olabilir yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-189">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="b4ef0-190">Merhaba uzantısı kaldırarak ve tercih ettiğiniz yürütme yöntemiyle hello uzantısı yeniden çalıştırma bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-190">You can do this by removing hello extension and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="b4ef0-191">bir uzantı tooremove komutu hello Azure PowerShell modülü ile aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-191">tooremove an extension, run hello following command with hello Azure PowerShell module.</span></span> <span data-ttu-id="b4ef0-192">Örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="b4ef0-193">Uzantı hello Azure portal kullanarak da kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-193">An extension can also be removed using hello Azure portal.</span></span> <span data-ttu-id="b4ef0-194">toodo için:</span><span class="sxs-lookup"><span data-stu-id="b4ef0-194">toodo so:</span></span>

1. <span data-ttu-id="b4ef0-195">Bir sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="b4ef0-196">Seçin **uzantıları**.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="b4ef0-197">İstenen hello uzantı seçin.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-197">Choose hello desired extension.</span></span>
4. <span data-ttu-id="b4ef0-198">Seçin **kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="b4ef0-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="b4ef0-199">Ortak VM uzantıları başvurusu</span><span class="sxs-lookup"><span data-stu-id="b4ef0-199">Common VM extensions reference</span></span>
| <span data-ttu-id="b4ef0-200">Uzantı adı</span><span class="sxs-lookup"><span data-stu-id="b4ef0-200">Extension name</span></span> | <span data-ttu-id="b4ef0-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b4ef0-201">Description</span></span> | <span data-ttu-id="b4ef0-202">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="b4ef0-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4ef0-203">Windows için özel betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="b4ef0-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="b4ef0-204">Bir Azure sanal makinesi karşı komut dosyalarını çalıştır</span><span class="sxs-lookup"><span data-stu-id="b4ef0-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="b4ef0-205">Windows için özel betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="b4ef0-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="b4ef0-206">Windows için DSC uzantısı</span><span class="sxs-lookup"><span data-stu-id="b4ef0-206">DSC Extension for Windows</span></span> |<span data-ttu-id="b4ef0-207">PowerShell DSC (İstenen durum Yapılandırması ') uzantısı</span><span class="sxs-lookup"><span data-stu-id="b4ef0-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="b4ef0-208">Windows için DSC uzantısı</span><span class="sxs-lookup"><span data-stu-id="b4ef0-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="b4ef0-209">Azure Tanılama Uzantısı</span><span class="sxs-lookup"><span data-stu-id="b4ef0-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="b4ef0-210">Azure tanılama yönetme</span><span class="sxs-lookup"><span data-stu-id="b4ef0-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="b4ef0-211">Azure Tanılama Uzantısı</span><span class="sxs-lookup"><span data-stu-id="b4ef0-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="b4ef0-212">Azure VM erişim uzantısı</span><span class="sxs-lookup"><span data-stu-id="b4ef0-212">Azure VM Access Extension</span></span> |<span data-ttu-id="b4ef0-213">Kullanıcılar ve kimlik bilgilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="b4ef0-213">Manage users and credentials</span></span> |[<span data-ttu-id="b4ef0-214">Linux VM erişim uzantısı</span><span class="sxs-lookup"><span data-stu-id="b4ef0-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
