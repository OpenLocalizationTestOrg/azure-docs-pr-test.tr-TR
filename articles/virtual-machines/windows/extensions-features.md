---
title: "Sanal makine uzantıları ve özellikleri Windows Azure için | Microsoft Docs"
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
ms.openlocfilehash: 1ce0eebd2585c9457d7f922898d7f2fa3e7ffad7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="e83f9-103">Sanal makine uzantıları ve özellikleri Windows için</span><span class="sxs-lookup"><span data-stu-id="e83f9-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="e83f9-104">Azure sanal makine uzantıları Azure sanal makinelerde dağıtım sonrası yapılandırma ve Otomasyon görevlerini sağlayan küçük uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="e83f9-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="e83f9-105">Örneğin, bir sanal makineye yazılım yükleme, virüsten koruma veya Docker yapılandırma gerektiriyorsa, bu görevleri tamamlamak için bir VM uzantısı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="e83f9-106">Azure VM uzantıları, Azure CLI, PowerShell, Azure Resource Manager şablonları ve Azure portalını kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e83f9-106">Azure VM extensions can be run by using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="e83f9-107">Uzantıları ile yeni bir sanal makine dağıtımı paketlenebilir veya varolan bir sistemle bağlantılı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e83f9-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="e83f9-108">Bu belge, sanal makine uzantıları, sanal makine uzantıları ve Kılavuzu algılamak, yönetmek ve sanal makine uzantıları kaldırmak nasıl kullanma önkoşulları genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="e83f9-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how to detect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="e83f9-109">Birçok VM uzantıları bulunduğundan, bu belgede genelleştirilmiş bilgiler sağlanmaktadır her potansiyel olarak benzersiz bir yapılandırmaya sahip.</span><span class="sxs-lookup"><span data-stu-id="e83f9-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="e83f9-110">Uzantıya özgü ayrıntıları her belge için ayrı ayrı uzantısı belirli bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="e83f9-111">Kullanım örnekleri ve örnekler</span><span class="sxs-lookup"><span data-stu-id="e83f9-111">Use cases and samples</span></span>

<span data-ttu-id="e83f9-112">Birçok farklı Azure VM uzantıları vardır, her biri belirli bir kullanım örneği.</span><span class="sxs-lookup"><span data-stu-id="e83f9-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="e83f9-113">Bazı örnek kullanım örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e83f9-113">Some example use cases are:</span></span>

- <span data-ttu-id="e83f9-114">PowerShell istenen durum yapılandırmalar için Windows DSC uzantısı kullanılarak bir sanal makine için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-114">Apply PowerShell Desired State configurations to a virtual machine by using the DSC extension for Windows.</span></span> <span data-ttu-id="e83f9-115">Daha fazla bilgi için bkz: [Azure istenen durum yapılandırması uzantısı](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e83f9-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="e83f9-116">Microsoft İzleme Aracısı VM uzantısı kullanarak sanal makine izlemeyi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e83f9-116">Configure virtual machine monitoring by using the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="e83f9-117">Daha fazla bilgi için bkz: [bağlanmak Azure sanal makineleri için günlük analizi](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e83f9-117">For more information, see [Connect Azure virtual machines to Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="e83f9-118">Azure altyapınızın Datadog uzantılı izlemeyi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e83f9-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="e83f9-119">Daha fazla bilgi için bkz: [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="e83f9-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="e83f9-120">Bir Azure sanal makinesi Chef kullanarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e83f9-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="e83f9-121">Daha fazla bilgi için bkz: [otomatikleştirme Azure sanal makine dağıtımı Chef ile](chef-automation.md).</span><span class="sxs-lookup"><span data-stu-id="e83f9-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="e83f9-122">İşleme özgü uzantılar ek olarak, bir özel betik uzantısı, Windows ve Linux sanal makineleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="e83f9-123">Windows için özel betik uzantısı, bir sanal makine üzerinde çalıştırılacak PowerShell komut dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e83f9-123">The Custom Script extension for Windows allows any PowerShell script to be run on a virtual machine.</span></span> <span data-ttu-id="e83f9-124">Yerel hangi Azure araçlar sağlayabilir ötesinde yapılandırma gerektiren Azure dağıtımları tasarlarken kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="e83f9-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="e83f9-125">Daha fazla bilgi için bkz: [Windows VM özel betik uzantısı](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="e83f9-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e83f9-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e83f9-126">Prerequisites</span></span>

<span data-ttu-id="e83f9-127">Her sanal makine uzantısı önkoşulları kendi kümesine sahip.</span><span class="sxs-lookup"><span data-stu-id="e83f9-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="e83f9-128">Örneğin, Docker VM uzantısı desteklenen Linux dağıtım önkoşul vardır.</span><span class="sxs-lookup"><span data-stu-id="e83f9-128">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="e83f9-129">Tek tek uzantıların gereksinimlerini uzantıya özgü belgelerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e83f9-129">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="e83f9-130">Azure VM aracısı</span><span class="sxs-lookup"><span data-stu-id="e83f9-130">Azure VM agent</span></span>
<span data-ttu-id="e83f9-131">Azure VM Aracısı bir Azure sanal makinesi ve Azure yapı denetleyicisi arasındaki etkileşimi yönetir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-131">The Azure VM agent manages interaction between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="e83f9-132">VM Aracısı dağıtma ve yönetme Azure sanal makineler, çalışan VM uzantıları dahil olmak üzere birçok işlevsel görünüşlere için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="e83f9-132">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="e83f9-133">Azure VM Aracısı Azure Marketi görüntülerinde önceden yüklenmiş ve desteklenen işletim sistemlerine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-133">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="e83f9-134">Desteklenen işletim sistemleri ve yükleme yönergeleri hakkında daha fazla bilgi için bkz: [Azure sanal makine Aracısı](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e83f9-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="e83f9-135">VM uzantıları Bul</span><span class="sxs-lookup"><span data-stu-id="e83f9-135">Discover VM extensions</span></span>
<span data-ttu-id="e83f9-136">Birçok farklı VM uzantıları, Azure sanal makineler ile kullanmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="e83f9-137">Tam listesini görmek için Azure Resource Manager PowerShell modülü ile aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e83f9-137">To see a complete list, run the following command with the Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="e83f9-138">Bu komutu çalıştırdığınızda istenen konumu belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e83f9-138">Make sure to specify the desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="e83f9-139">VM uzantıları çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e83f9-139">Run VM extensions</span></span>

<span data-ttu-id="e83f9-140">Azure sanal makine uzantıları yapılandırma değişikliklerini yapın veya zaten dağıtılmış bir VM'de bağlantısı kurtarmak gerektiğinde faydalı olan mevcut sanal makinelerde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="e83f9-141">VM uzantıları, Azure Resource Manager şablonu dağıtımlarında da gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="e83f9-142">Resource Manager şablonları ile uzantıları kullanarak, dağıtılması ve dağıtım sonrası müdahalesi gerektirmeden yapılandırılmış için Azure sanal makineleri etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e83f9-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines to be deployed and configured without the need for post-deployment intervention.</span></span>

<span data-ttu-id="e83f9-143">Aşağıdaki yöntemlerden bir uzantısı olan bir sanal makineyi karşı çalıştırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-143">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="e83f9-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e83f9-144">PowerShell</span></span>

<span data-ttu-id="e83f9-145">Birkaç PowerShell komutları tek tek uzantıların çalıştırmak için mevcut.</span><span class="sxs-lookup"><span data-stu-id="e83f9-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="e83f9-146">Bir listesini görmek için aşağıdaki PowerShell komutlarını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e83f9-146">To see a list, run the following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="e83f9-147">Bu, aşağıdakine benzer bir çıktı sağlar:</span><span class="sxs-lookup"><span data-stu-id="e83f9-147">This provides output similar to the following:</span></span>

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

<span data-ttu-id="e83f9-148">Aşağıdaki örnek, bir komut dosyası hedef sanal makine üzerine GitHub deposunu indirin ve komut dosyasını çalıştırmak için özel betik uzantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="e83f9-148">The following example uses the Custom Script extension to download a script from a GitHub repository onto the target virtual machine and then run the script.</span></span> <span data-ttu-id="e83f9-149">Özel betik uzantısı hakkında daha fazla bilgi için bkz: [özel betik uzantısı genel bakış](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="e83f9-149">For more information on the Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="e83f9-150">Bu örnekte, VM erişim uzantısı, Windows sanal makine yönetici parolasını sıfırlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e83f9-150">In this example, the VM Access extension is used to reset the administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="e83f9-151">VM erişim uzantısı ile ilgili daha fazla bilgi için bkz: [Windows VM Uzak Masaüstü'nü Sıfırla Hizmeti'nde](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="e83f9-151">For more information on the VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="e83f9-152">`Set-AzureRmVMExtension` Komutu, tüm VM uzantısı başlatmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-152">The `Set-AzureRmVMExtension` command can be used to start any VM extension.</span></span> <span data-ttu-id="e83f9-153">Daha fazla bilgi için bkz: [kümesi AzureRmVMExtension başvuru](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="e83f9-153">For more information, see the [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="e83f9-154">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="e83f9-154">Azure portal</span></span>

<span data-ttu-id="e83f9-155">VM uzantısı olan bir sanal makineyi Azure Portalı aracılığıyla uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-155">A VM extension can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="e83f9-156">Bunu yapmak için kullanmak, seçmek istediğiniz sanal makineyi seçin **uzantıları**, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e83f9-156">To do so, select the virtual machine you want to use, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="e83f9-157">Bu, kullanılabilir uzantıları listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="e83f9-157">This provides a list of available extensions.</span></span> <span data-ttu-id="e83f9-158">İstediğiniz ve sihirbazdaki adımları izleyin birini seçin.</span><span class="sxs-lookup"><span data-stu-id="e83f9-158">Select the one you want and follow the steps in the wizard.</span></span>

<span data-ttu-id="e83f9-159">Aşağıdaki resim Azure portalından Microsoft Antimalware uzantının yüklenmesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-159">The following image shows the installation of the Microsoft Antimalware extension from the Azure portal.</span></span>

![Kötü amaçlı yazılımdan koruma uzantısını yükleyin](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="e83f9-161">Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="e83f9-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="e83f9-162">VM uzantıları, bir Azure Resource Manager şablonu eklenir ve şablon dağıtımı ile yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="e83f9-162">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="e83f9-163">Bir şablonla uzantıları tam olarak yapılandırılmış Azure dağıtımları oluşturmak için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="e83f9-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="e83f9-164">Örneğin, aşağıdaki JSON yük dengeli sanal makineler kümesi ve Azure SQL Veritabanını dağıtır ve ardından her VM .NET Core uygulama yükleyen bir Resource Manager şablonu alınır.</span><span class="sxs-lookup"><span data-stu-id="e83f9-164">For example, the following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="e83f9-165">VM uzantısı yazılım yüklemesi mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="e83f9-165">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="e83f9-166">Daha fazla bilgi için bkz: [tam Resource Manager şablonu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="e83f9-166">For more information, see the [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

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

<span data-ttu-id="e83f9-167">Daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma Windows VM uzantıları ile](template-description.md#extensions).</span><span class="sxs-lookup"><span data-stu-id="e83f9-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="e83f9-168">VM uzantısı verileri güvenli</span><span class="sxs-lookup"><span data-stu-id="e83f9-168">Secure VM extension data</span></span>

<span data-ttu-id="e83f9-169">VM uzantısı çalıştırırken kimlik bilgilerini, depolama hesabı adları ve depolama hesabı erişim anahtarlarını gibi hassas bilgiler dahil etmek gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-169">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="e83f9-170">Birçok VM uzantıları verileri şifreler ve yalnızca hedef sanal makine içinde şifresini çözer korumalı bir yapılandırmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="e83f9-171">Her bir uzantı uzantıya özgü belgelerinde ayrıntılı bir belirli korumalı yapılandırma şeması vardır.</span><span class="sxs-lookup"><span data-stu-id="e83f9-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="e83f9-172">Aşağıdaki örnek, Windows için özel betik uzantısı örneğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-172">The following example shows an instance of the Custom Script extension for Windows.</span></span> <span data-ttu-id="e83f9-173">Komutun yürütülmesi için kimlik bilgileri kümesini içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e83f9-173">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="e83f9-174">Bu örnekte, yürütülecek komut şifrelenmez.</span><span class="sxs-lookup"><span data-stu-id="e83f9-174">In this example, the command to execute will not be encrypted.</span></span>


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

<span data-ttu-id="e83f9-175">Yürütme dize taşıyarak güvenli **yürütülecek komut** özelliğine **korumalı** yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="e83f9-175">Secure the execution string by moving the **command to execute** property to the **protected** configuration.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="e83f9-176">VM uzantıları sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e83f9-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="e83f9-177">Her VM uzantısı özel sorun giderme adımları olabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="e83f9-178">Örneğin, özel betik uzantısı kullanırken, komut dosyası yürütme ayrıntılarını yerel olarak sanal makinede uzantı çalıştırıldı bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-178">For instance, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="e83f9-179">Uzantı özel sorun giderme işlemleri uzantıya özgü belgelerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e83f9-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="e83f9-180">Tüm sanal makine uzantıları için aşağıdaki sorun giderme adımlarını uygulayın.</span><span class="sxs-lookup"><span data-stu-id="e83f9-180">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="e83f9-181">Uzantı durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="e83f9-181">View extension status</span></span>

<span data-ttu-id="e83f9-182">Bir sanal makine uzantısı bir sanal makine çalıştırdıktan sonra uzantı durumunu döndürmek için aşağıdaki PowerShell komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e83f9-182">After a virtual machine extension has been run against a virtual machine, use the following PowerShell command to return extension status.</span></span> <span data-ttu-id="e83f9-183">Örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e83f9-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="e83f9-184">`Name` Parametresi, yürütme esnasında uzantısını verilen ad alır.</span><span class="sxs-lookup"><span data-stu-id="e83f9-184">The `Name` parameter takes the name given to the extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="e83f9-185">Çıktı aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="e83f9-185">The output looks like the following:</span></span>

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

<span data-ttu-id="e83f9-186">Uzantı yürütme durumu de Azure portalında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-186">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="e83f9-187">Uzantı durumunu görüntülemek için sanal makineyi seçin, **uzantıları**ve istenen uzantı seçin.</span><span class="sxs-lookup"><span data-stu-id="e83f9-187">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="e83f9-188">VM uzantıları yeniden çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e83f9-188">Rerun VM extensions</span></span>

<span data-ttu-id="e83f9-189">Bir sanal makine uzantısı yeniden çalıştırılması gereken durumlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-189">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="e83f9-190">Uzantı kaldırarak ve tercih ettiğiniz yürütme yöntemiyle uzantısı yeniden çalıştırma bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e83f9-190">You can do this by removing the extension and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="e83f9-191">Bir uzantıyı kaldırmak için Azure PowerShell modülü ile aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e83f9-191">To remove an extension, run the following command with the Azure PowerShell module.</span></span> <span data-ttu-id="e83f9-192">Örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e83f9-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="e83f9-193">Uzantı, Azure portalını kullanarak da kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e83f9-193">An extension can also be removed using the Azure portal.</span></span> <span data-ttu-id="e83f9-194">Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="e83f9-194">To do so:</span></span>

1. <span data-ttu-id="e83f9-195">Bir sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="e83f9-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="e83f9-196">Seçin **uzantıları**.</span><span class="sxs-lookup"><span data-stu-id="e83f9-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="e83f9-197">İstenen uzantı seçin.</span><span class="sxs-lookup"><span data-stu-id="e83f9-197">Choose the desired extension.</span></span>
4. <span data-ttu-id="e83f9-198">Seçin **kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="e83f9-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="e83f9-199">Ortak VM uzantıları başvurusu</span><span class="sxs-lookup"><span data-stu-id="e83f9-199">Common VM extensions reference</span></span>
| <span data-ttu-id="e83f9-200">Uzantı adı</span><span class="sxs-lookup"><span data-stu-id="e83f9-200">Extension name</span></span> | <span data-ttu-id="e83f9-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e83f9-201">Description</span></span> | <span data-ttu-id="e83f9-202">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="e83f9-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e83f9-203">Windows için özel betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="e83f9-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="e83f9-204">Bir Azure sanal makinesi karşı komut dosyalarını çalıştır</span><span class="sxs-lookup"><span data-stu-id="e83f9-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="e83f9-205">Windows için özel betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="e83f9-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="e83f9-206">Windows için DSC uzantısı</span><span class="sxs-lookup"><span data-stu-id="e83f9-206">DSC Extension for Windows</span></span> |<span data-ttu-id="e83f9-207">PowerShell DSC (İstenen durum Yapılandırması ') uzantısı</span><span class="sxs-lookup"><span data-stu-id="e83f9-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="e83f9-208">Windows için DSC uzantısı</span><span class="sxs-lookup"><span data-stu-id="e83f9-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="e83f9-209">Azure Tanılama Uzantısı</span><span class="sxs-lookup"><span data-stu-id="e83f9-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="e83f9-210">Azure tanılama yönetme</span><span class="sxs-lookup"><span data-stu-id="e83f9-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="e83f9-211">Azure Tanılama Uzantısı</span><span class="sxs-lookup"><span data-stu-id="e83f9-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="e83f9-212">Azure VM erişim uzantısı</span><span class="sxs-lookup"><span data-stu-id="e83f9-212">Azure VM Access Extension</span></span> |<span data-ttu-id="e83f9-213">Kullanıcılar ve kimlik bilgilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="e83f9-213">Manage users and credentials</span></span> |[<span data-ttu-id="e83f9-214">Linux VM erişim uzantısı</span><span class="sxs-lookup"><span data-stu-id="e83f9-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
