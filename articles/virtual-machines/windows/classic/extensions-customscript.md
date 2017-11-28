---
title: "aaaCustom Windows VM betik uzantısı | Microsoft Docs"
description: "Uzak bir Windows VM hello özel betik uzantısı toorun PowerShell komut dosyalarını kullanarak Azure VM yapılandırma görevleri otomatikleştirme"
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
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a><span data-ttu-id="eba72-103">Özel betik uzantısı hello Klasik dağıtım modeli kullanılarak Windows için</span><span class="sxs-lookup"><span data-stu-id="eba72-103">Custom Script Extension for Windows using hello classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="eba72-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="eba72-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="eba72-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="eba72-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="eba72-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="eba72-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="eba72-107">Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eba72-107">Learn how too[perform these steps using hello Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="eba72-108">Merhaba özel betik uzantısının indirir ve Azure sanal makinelerde komut dosyalarını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="eba72-108">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="eba72-109">Bu dağıtım yapılandırmaları, yazılım yükleme veya başka bir yapılandırma için yararlı bir uzantısıdır / yönetim görevi.</span><span class="sxs-lookup"><span data-stu-id="eba72-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="eba72-110">Komut dosyaları Azure depolama veya GitHub indirilen veya toohello çalışma zamanı uzantısı Azure portalında sağlanan.</span><span class="sxs-lookup"><span data-stu-id="eba72-110">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="eba72-111">Merhaba özel betik uzantısı Azure Resource Manager şablonları ile tümleşir ve hello Azure CLI, PowerShell, Azure portal veya hello Azure sanal makine REST API'sini kullanarak da çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="eba72-111">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="eba72-112">Bu belge nasıl toouse hello özel betik uzantısı kullanılarak hello Azure PowerShell modülü, Azure Resource Manager şablonları ve sorun giderme adımları Windows sistemlerinde ayrıntıları ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="eba72-112">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eba72-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eba72-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="eba72-114">İşletim Sistemi</span><span class="sxs-lookup"><span data-stu-id="eba72-114">Operating System</span></span>

<span data-ttu-id="eba72-115">Windows, Windows Server 2008 R2 karşı çalıştırılabilir için hello özel betik uzantısının 2012, 2012 R2 ve 2016 serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="eba72-115">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="eba72-116">Komut dosyası konumu</span><span class="sxs-lookup"><span data-stu-id="eba72-116">Script Location</span></span>

<span data-ttu-id="eba72-117">Merhaba komut dosyası Azure depolama veya başka bir konuma geçerli bir URL ile erişilebilir depolanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="eba72-117">hello script needs toobe stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="eba72-118">Internet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="eba72-118">Internet Connectivity</span></span>

<span data-ttu-id="eba72-119">Merhaba özel betik uzantısı için Windows hello hedef sanal makinenin bağlı toohello gerektirir Internet.</span><span class="sxs-lookup"><span data-stu-id="eba72-119">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="eba72-120">Uzantı Şeması</span><span class="sxs-lookup"><span data-stu-id="eba72-120">Extension schema</span></span>

<span data-ttu-id="eba72-121">Merhaba aşağıdaki JSON hello özel betik uzantısının hello şemasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="eba72-121">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="eba72-122">Merhaba uzantısı, bir komut dosyası konumuna (Azure Storage veya başka bir konuma geçerli bir URL ile) ve komut tooexecute gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eba72-122">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="eba72-123">Azure Storage hello komut dosyası kaynağı olarak kullanıyorsanız, bir Azure depolama hesabı adı ve hesap anahtarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="eba72-123">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="eba72-124">Bu öğeler hassas verisi olarak kabul edilir ve hello uzantıları korumalı ayarını yapılandırma dosyasında belirtilen.</span><span class="sxs-lookup"><span data-stu-id="eba72-124">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="eba72-125">Azure VM uzantısının korumalı ayarı veri şifrelenir ve yalnızca hello hedef sanal makineye şifresi.</span><span class="sxs-lookup"><span data-stu-id="eba72-125">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="eba72-126">Özellik değerleri</span><span class="sxs-lookup"><span data-stu-id="eba72-126">Property values</span></span>

| <span data-ttu-id="eba72-127">Ad</span><span class="sxs-lookup"><span data-stu-id="eba72-127">Name</span></span> | <span data-ttu-id="eba72-128">Değer / örnek</span><span class="sxs-lookup"><span data-stu-id="eba72-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="eba72-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="eba72-129">apiVersion</span></span> | <span data-ttu-id="eba72-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="eba72-130">2015-06-15</span></span> |
| <span data-ttu-id="eba72-131">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="eba72-131">publisher</span></span> | <span data-ttu-id="eba72-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="eba72-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="eba72-133">Uzantısı</span><span class="sxs-lookup"><span data-stu-id="eba72-133">extension</span></span> | <span data-ttu-id="eba72-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="eba72-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="eba72-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="eba72-135">typeHandlerVersion</span></span> | <span data-ttu-id="eba72-136">1.8</span><span class="sxs-lookup"><span data-stu-id="eba72-136">1.8</span></span> |
| <span data-ttu-id="eba72-137">fileUris (örneğin)</span><span class="sxs-lookup"><span data-stu-id="eba72-137">fileUris (e.g)</span></span> | <span data-ttu-id="eba72-138">https://RAW.githubusercontent.com/Microsoft/dotnet-Core-Sample-Templates/master/dotnet-Core-Music-Windows/scripts/Configure-Music-App.ps1</span><span class="sxs-lookup"><span data-stu-id="eba72-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="eba72-139">commandToExecute (örneğin)</span><span class="sxs-lookup"><span data-stu-id="eba72-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="eba72-140">PowerShell - ExecutionPolicy Unrestricted - dosya yapılandırma-müzik-app.ps1</span><span class="sxs-lookup"><span data-stu-id="eba72-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="eba72-141">Şablon dağıtımı</span><span class="sxs-lookup"><span data-stu-id="eba72-141">Template deployment</span></span>

<span data-ttu-id="eba72-142">Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="eba72-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="eba72-143">Merhaba JSON şeması Hello önceki bölümde ayrıntılı bir Azure Resource Manager şablon dağıtımı sırasında bir Azure Resource Manager şablonu toorun hello özel betik uzantısı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eba72-143">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="eba72-144">Özel betik uzantısının burada bulunabilir hello içeren bir örnek şablonunu [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="eba72-144">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="eba72-145">PowerShell dağıtım</span><span class="sxs-lookup"><span data-stu-id="eba72-145">PowerShell deployment</span></span>

<span data-ttu-id="eba72-146">Merhaba `Set-AzureVMCustomScriptExtension` komutu kullanılan tooadd hello özel betik uzantısı tooan varolan sanal makine olabilir.</span><span class="sxs-lookup"><span data-stu-id="eba72-146">hello `Set-AzureVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="eba72-147">Daha fazla bilgi için bkz: [kümesi AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="eba72-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="eba72-148">Sorun giderme ve Destek</span><span class="sxs-lookup"><span data-stu-id="eba72-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="eba72-149">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="eba72-149">Troubleshoot</span></span>

<span data-ttu-id="eba72-150">Veri uzantısı dağıtımları hello durumuyla ilgili hello Azure portal ve hello Azure PowerShell modülü kullanılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="eba72-150">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="eba72-151">toosee hello dağıtım durumu hello aşağıdaki komutu çalıştırın, belirli bir VM için uzantıları.</span><span class="sxs-lookup"><span data-stu-id="eba72-151">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="eba72-152">Uzantı yürütme bize dizin hello hedef sanal makinede aşağıdaki hello bulunan oturum toofiles çıktı.</span><span class="sxs-lookup"><span data-stu-id="eba72-152">Extension execution output us logged toofiles found in hello following directory on hello target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="eba72-153">Merhaba komut dosyasının kendisini dizin hello hedef sanal makinede aşağıdaki hello içine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="eba72-153">hello script itself is downloaded into hello following directory on hello target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="eba72-154">Destek</span><span class="sxs-lookup"><span data-stu-id="eba72-154">Support</span></span>

<span data-ttu-id="eba72-155">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz hello Azure uzmanlarıyla hello [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="eba72-155">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="eba72-156">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="eba72-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="eba72-157">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin.</span><span class="sxs-lookup"><span data-stu-id="eba72-157">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="eba72-158">Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="eba72-158">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
