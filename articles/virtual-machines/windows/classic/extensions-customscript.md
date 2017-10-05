---
title: "Bir Windows VM özel betik uzantısı | Microsoft Docs"
description: "Uzak bir Windows VM PowerShell betikleri çalıştırmak için özel betik uzantısı kullanarak Azure VM yapılandırma görevleri otomatikleştirme"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: 986ab1025dc188cd7fa1cf8b131a9d4b859be8f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="custom-script-extension-for-windows-using-the-classic-deployment-model"></a><span data-ttu-id="95514-103">Özel betik uzantısı Klasik dağıtım modeli kullanılarak Windows için</span><span class="sxs-lookup"><span data-stu-id="95514-103">Custom Script Extension for Windows using the classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="95514-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="95514-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="95514-105">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="95514-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="95514-106">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="95514-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="95514-107">[Bu adımları Resource Manager modeli kullanarak gerçekleştirmeyi](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) öğrenin.</span><span class="sxs-lookup"><span data-stu-id="95514-107">Learn how to [perform these steps using the Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="95514-108">Özel betik uzantısının indirir ve Azure sanal makinelerde komut dosyaları çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="95514-108">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="95514-109">Bu dağıtım yapılandırmaları, yazılım yükleme veya başka bir yapılandırma için yararlı bir uzantısıdır / yönetim görevi.</span><span class="sxs-lookup"><span data-stu-id="95514-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="95514-110">Komut dosyaları Azure depolama veya GitHub indirilen veya çalışma zamanı uzantısı Azure portalında sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="95514-110">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="95514-111">Özel betik uzantısı, Azure Resource Manager şablonları ile tümleşir ve Azure CLI, PowerShell, Azure portalında veya Azure sanal makine REST API'sini kullanarak da çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="95514-111">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="95514-112">Bu belge Azure PowerShell modülü, Azure Resource Manager şablonları ve sorun giderme adımları Windows sistemlerinde ayrıntıları kullanarak özel betik uzantısı kullanma ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="95514-112">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95514-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="95514-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="95514-114">İşletim Sistemi</span><span class="sxs-lookup"><span data-stu-id="95514-114">Operating System</span></span>

<span data-ttu-id="95514-115">Windows, Windows Server 2008 R2 karşı çalıştırılabilir için özel betik uzantısının 2012, 2012 R2 ve 2016 serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="95514-115">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="95514-116">Komut dosyası konumu</span><span class="sxs-lookup"><span data-stu-id="95514-116">Script Location</span></span>

<span data-ttu-id="95514-117">Komut dosyası Azure depolama veya başka bir konuma geçerli bir URL ile erişilebilir depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="95514-117">The script needs to be stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="95514-118">Internet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="95514-118">Internet Connectivity</span></span>

<span data-ttu-id="95514-119">Windows için özel betik uzantısı hedef sanal makine internet'e bağlı olduğunu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="95514-119">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="95514-120">Uzantı Şeması</span><span class="sxs-lookup"><span data-stu-id="95514-120">Extension schema</span></span>

<span data-ttu-id="95514-121">Aşağıdaki JSON şeması özel betik uzantısı gösterir.</span><span class="sxs-lookup"><span data-stu-id="95514-121">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="95514-122">Uzantısı için bir komut dosyası konumuna (Azure Storage veya başka bir konuma geçerli bir URL ile) ve bir komutun yürütülmesi için gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="95514-122">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="95514-123">Azure Storage komut dosyası kaynağı olarak kullanıyorsanız, bir Azure depolama hesabı adı ve hesap anahtarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="95514-123">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="95514-124">Bu öğeler hassas verisi olarak kabul edilir ve uzantıları korumalı ayarı yapılandırmasında belirtilen.</span><span class="sxs-lookup"><span data-stu-id="95514-124">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="95514-125">Azure VM uzantısının korumalı ayarı veri şifrelenir ve yalnızca hedef sanal makineye şifresi.</span><span class="sxs-lookup"><span data-stu-id="95514-125">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="95514-126">Özellik değerleri</span><span class="sxs-lookup"><span data-stu-id="95514-126">Property values</span></span>

| <span data-ttu-id="95514-127">Ad</span><span class="sxs-lookup"><span data-stu-id="95514-127">Name</span></span> | <span data-ttu-id="95514-128">Değer / örnek</span><span class="sxs-lookup"><span data-stu-id="95514-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="95514-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="95514-129">apiVersion</span></span> | <span data-ttu-id="95514-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="95514-130">2015-06-15</span></span> |
| <span data-ttu-id="95514-131">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="95514-131">publisher</span></span> | <span data-ttu-id="95514-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="95514-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="95514-133">Uzantısı</span><span class="sxs-lookup"><span data-stu-id="95514-133">extension</span></span> | <span data-ttu-id="95514-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="95514-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="95514-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="95514-135">typeHandlerVersion</span></span> | <span data-ttu-id="95514-136">1.8</span><span class="sxs-lookup"><span data-stu-id="95514-136">1.8</span></span> |
| <span data-ttu-id="95514-137">fileUris (örneğin)</span><span class="sxs-lookup"><span data-stu-id="95514-137">fileUris (e.g)</span></span> | <span data-ttu-id="95514-138">https://RAW.githubusercontent.com/Microsoft/dotnet-Core-Sample-Templates/master/dotnet-Core-Music-Windows/scripts/Configure-Music-App.ps1</span><span class="sxs-lookup"><span data-stu-id="95514-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="95514-139">commandToExecute (örneğin)</span><span class="sxs-lookup"><span data-stu-id="95514-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="95514-140">PowerShell - ExecutionPolicy Unrestricted - dosya yapılandırma-müzik-app.ps1</span><span class="sxs-lookup"><span data-stu-id="95514-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="95514-141">Şablon dağıtımı</span><span class="sxs-lookup"><span data-stu-id="95514-141">Template deployment</span></span>

<span data-ttu-id="95514-142">Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="95514-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="95514-143">Önceki bölümde ayrıntılı JSON şeması bir Azure Resource Manager şablonunda bir Azure Resource Manager şablon dağıtımı sırasında özel betik uzantısının çalıştırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="95514-143">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="95514-144">Özel betik uzantısı içeren bir örnek şablonu burada bulunabilir [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="95514-144">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="95514-145">PowerShell dağıtım</span><span class="sxs-lookup"><span data-stu-id="95514-145">PowerShell deployment</span></span>

<span data-ttu-id="95514-146">`Set-AzureVMCustomScriptExtension` Komutu, varolan bir sanal makineye özel betik uzantısı eklemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="95514-146">The `Set-AzureVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="95514-147">Daha fazla bilgi için bkz: [kümesi AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="95514-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="95514-148">Sorun giderme ve Destek</span><span class="sxs-lookup"><span data-stu-id="95514-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="95514-149">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="95514-149">Troubleshoot</span></span>

<span data-ttu-id="95514-150">Veri uzantısı dağıtımları durumuyla ilgili Azure portalından ve Azure PowerShell modülü kullanılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="95514-150">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="95514-151">İçin belirli bir VM uzantıları dağıtım durumunu görmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="95514-151">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="95514-152">Uzantı yürütme bize hedef sanal makinede aşağıdaki dizinde bulunan dosyaları oturum çıktı.</span><span class="sxs-lookup"><span data-stu-id="95514-152">Extension execution output us logged to files found in the following directory on the target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="95514-153">Betik hedef sanal makinedeki şu dizine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="95514-153">The script itself is downloaded into the following directory on the target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="95514-154">Destek</span><span class="sxs-lookup"><span data-stu-id="95514-154">Support</span></span>

<span data-ttu-id="95514-155">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, üzerinde Azure uzmanlar başvurabilirsiniz [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="95514-155">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="95514-156">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="95514-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="95514-157">Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin.</span><span class="sxs-lookup"><span data-stu-id="95514-157">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="95514-158">Azure desteği hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="95514-158">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>