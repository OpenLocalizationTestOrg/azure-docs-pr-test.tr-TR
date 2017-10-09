---
title: "Windows için özel betik uzantısı aaaAzure | Microsoft Docs"
description: "Merhaba özel betik uzantısı kullanarak Windows VM yapılandırma görevleri otomatikleştirme"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="60c66-103">Windows için özel betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="60c66-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="60c66-104">Merhaba özel betik uzantısının indirir ve Azure sanal makinelerde komut dosyalarını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="60c66-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="60c66-105">Bu dağıtım yapılandırmaları, yazılım yükleme veya başka bir yapılandırma için yararlı bir uzantısıdır / yönetim görevi.</span><span class="sxs-lookup"><span data-stu-id="60c66-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="60c66-106">Komut dosyaları Azure depolama veya GitHub indirilen veya toohello çalışma zamanı uzantısı Azure portalında sağlanan.</span><span class="sxs-lookup"><span data-stu-id="60c66-106">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="60c66-107">Merhaba özel betik uzantısı Azure Resource Manager şablonları ile tümleşir ve hello Azure CLI, PowerShell, Azure portal veya hello Azure sanal makine REST API'sini kullanarak da çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="60c66-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="60c66-108">Bu belge nasıl toouse hello özel betik uzantısı kullanılarak hello Azure PowerShell modülü, Azure Resource Manager şablonları ve sorun giderme adımları Windows sistemlerinde ayrıntıları ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="60c66-108">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60c66-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="60c66-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="60c66-110">İşletim Sistemi</span><span class="sxs-lookup"><span data-stu-id="60c66-110">Operating System</span></span>

<span data-ttu-id="60c66-111">Windows, Windows Server 2008 R2 karşı çalıştırılabilir için hello özel betik uzantısının 2012, 2012 R2 ve 2016 serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="60c66-111">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="60c66-112">Komut dosyası konumu</span><span class="sxs-lookup"><span data-stu-id="60c66-112">Script Location</span></span>

<span data-ttu-id="60c66-113">Merhaba komut dosyası Azure Blob Depolama veya başka bir konuma geçerli bir URL ile erişilebilir depolanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="60c66-113">hello script needs toobe stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="60c66-114">Internet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="60c66-114">Internet Connectivity</span></span>

<span data-ttu-id="60c66-115">Merhaba özel betik uzantısı için Windows hello hedef sanal makinenin bağlı toohello gerektirir Internet.</span><span class="sxs-lookup"><span data-stu-id="60c66-115">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="60c66-116">Uzantı Şeması</span><span class="sxs-lookup"><span data-stu-id="60c66-116">Extension schema</span></span>

<span data-ttu-id="60c66-117">Merhaba aşağıdaki JSON hello özel betik uzantısının hello şemasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="60c66-117">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="60c66-118">Merhaba uzantısı, bir komut dosyası konumuna (Azure Storage veya başka bir konuma geçerli bir URL ile) ve komut tooexecute gerektirir.</span><span class="sxs-lookup"><span data-stu-id="60c66-118">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="60c66-119">Azure Storage hello komut dosyası kaynağı olarak kullanıyorsanız, bir Azure depolama hesabı adı ve hesap anahtarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="60c66-119">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="60c66-120">Bu öğeler hassas verisi olarak kabul edilir ve hello uzantıları korumalı ayarını yapılandırma dosyasında belirtilen.</span><span class="sxs-lookup"><span data-stu-id="60c66-120">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="60c66-121">Azure VM uzantısının korumalı ayarı veri şifrelenir ve yalnızca hello hedef sanal makineye şifresi.</span><span class="sxs-lookup"><span data-stu-id="60c66-121">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

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
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="60c66-122">Özellik değerleri</span><span class="sxs-lookup"><span data-stu-id="60c66-122">Property values</span></span>

| <span data-ttu-id="60c66-123">Ad</span><span class="sxs-lookup"><span data-stu-id="60c66-123">Name</span></span> | <span data-ttu-id="60c66-124">Değer / örnek</span><span class="sxs-lookup"><span data-stu-id="60c66-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="60c66-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="60c66-125">apiVersion</span></span> | <span data-ttu-id="60c66-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="60c66-126">2015-06-15</span></span> |
| <span data-ttu-id="60c66-127">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="60c66-127">publisher</span></span> | <span data-ttu-id="60c66-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="60c66-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="60c66-129">type</span><span class="sxs-lookup"><span data-stu-id="60c66-129">type</span></span> | <span data-ttu-id="60c66-130">Uzantıları</span><span class="sxs-lookup"><span data-stu-id="60c66-130">extensions</span></span> |
| <span data-ttu-id="60c66-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="60c66-131">typeHandlerVersion</span></span> | <span data-ttu-id="60c66-132">1.9</span><span class="sxs-lookup"><span data-stu-id="60c66-132">1.9</span></span> |
| <span data-ttu-id="60c66-133">fileUris (örneğin)</span><span class="sxs-lookup"><span data-stu-id="60c66-133">fileUris (e.g)</span></span> | <span data-ttu-id="60c66-134">https://RAW.githubusercontent.com/Microsoft/dotnet-Core-Sample-Templates/master/dotnet-Core-Music-Windows/scripts/Configure-Music-App.ps1</span><span class="sxs-lookup"><span data-stu-id="60c66-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="60c66-135">commandToExecute (örneğin)</span><span class="sxs-lookup"><span data-stu-id="60c66-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="60c66-136">PowerShell - ExecutionPolicy Unrestricted - dosya yapılandırma-müzik-app.ps1</span><span class="sxs-lookup"><span data-stu-id="60c66-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="60c66-137">storageAccountName (örneğin)</span><span class="sxs-lookup"><span data-stu-id="60c66-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="60c66-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="60c66-138">examplestorageacct</span></span> |
| <span data-ttu-id="60c66-139">storageAccountKey (örneğin)</span><span class="sxs-lookup"><span data-stu-id="60c66-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="60c66-140">TmJK/1N3AbAZ3q / + hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg ==</span><span class="sxs-lookup"><span data-stu-id="60c66-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="60c66-141">**Not** -bu özellik adları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="60c66-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="60c66-142">Tooavoid dağıtım sorunlarını görüldüğü gibi Hello adları kullanın.</span><span class="sxs-lookup"><span data-stu-id="60c66-142">Use hello names as seen above tooavoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="60c66-143">Şablon dağıtımı</span><span class="sxs-lookup"><span data-stu-id="60c66-143">Template deployment</span></span>

<span data-ttu-id="60c66-144">Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="60c66-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="60c66-145">Merhaba JSON şeması Hello önceki bölümde ayrıntılı bir Azure Resource Manager şablon dağıtımı sırasında bir Azure Resource Manager şablonu toorun hello özel betik uzantısı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="60c66-145">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="60c66-146">Özel betik uzantısının burada bulunabilir hello içeren bir örnek şablonunu [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="60c66-146">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="60c66-147">PowerShell dağıtım</span><span class="sxs-lookup"><span data-stu-id="60c66-147">PowerShell deployment</span></span>

<span data-ttu-id="60c66-148">Merhaba `Set-AzureRmVMCustomScriptExtension` komutu kullanılan tooadd hello özel betik uzantısı tooan varolan sanal makine olabilir.</span><span class="sxs-lookup"><span data-stu-id="60c66-148">hello `Set-AzureRmVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="60c66-149">Daha fazla bilgi için bkz: [kümesi AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="60c66-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="60c66-150">Sorun giderme ve Destek</span><span class="sxs-lookup"><span data-stu-id="60c66-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="60c66-151">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="60c66-151">Troubleshoot</span></span>

<span data-ttu-id="60c66-152">Veri uzantısı dağıtımları hello durumuyla ilgili hello Azure portal ve hello Azure PowerShell modülü kullanılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="60c66-152">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="60c66-153">toosee hello dağıtım durumu hello aşağıdaki komutu çalıştırın, belirli bir VM için uzantıları.</span><span class="sxs-lookup"><span data-stu-id="60c66-153">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="60c66-154">Uzantı yürütme hello altında bulunan oturum toofiles dizin hello hedef sanal makinede aşağıdaki çıktı.</span><span class="sxs-lookup"><span data-stu-id="60c66-154">Extension execution output is logged toofiles found under hello following directory on hello target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="60c66-155">Merhaba, dizin hello hedef sanal makinede aşağıdaki hello içine indirilen dosyaları belirtilen.</span><span class="sxs-lookup"><span data-stu-id="60c66-155">hello specified files are downloaded into hello following directory on hello target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="60c66-156">Burada `<n>` hangi hello uzantısı yürütmeleri arasında değişebilir ondalık bir tamsayıdır.</span><span class="sxs-lookup"><span data-stu-id="60c66-156">where `<n>` is a decimal integer which may change between executions of hello extension.</span></span>  <span data-ttu-id="60c66-157">Merhaba `1.*` değerle hello gerçek, geçerli `typeHandlerVersion` hello uzantısı değeri.</span><span class="sxs-lookup"><span data-stu-id="60c66-157">hello `1.*` value matches hello actual, current `typeHandlerVersion` value of hello extension.</span></span>  <span data-ttu-id="60c66-158">Örneğin, hello gerçek dizin olabilir `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="60c66-158">For example, hello actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="60c66-159">Merhaba yürütülürken `commandToExecute` komutunu hello uzantısına ayarlayacak bu dizin (örneğin, `...\Downloads\2`) hello geçerli çalışma dizini olarak.</span><span class="sxs-lookup"><span data-stu-id="60c66-159">When executing hello `commandToExecute` command, hello extension will have set this directory (e.g., `...\Downloads\2`) as hello current working directory.</span></span> <span data-ttu-id="60c66-160">İndirilen bu etkinleştirir hello kullan göreli yollar toolocate hello dosyaların hello `fileURIs` özelliği.</span><span class="sxs-lookup"><span data-stu-id="60c66-160">This enables hello use of relative paths toolocate hello files downloaded via hello `fileURIs` property.</span></span> <span data-ttu-id="60c66-161">Merhaba örnekler için aşağıdaki tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="60c66-161">See hello table below for examples.</span></span>

<span data-ttu-id="60c66-162">Merhaba mutlak indirme yolunu zaman içinde değişebildiğinden hello yollarında göreli komut dosyası için daha iyi tooopt olan `commandToExecute` , mümkün olduğunda dize.</span><span class="sxs-lookup"><span data-stu-id="60c66-162">Since hello absolute download path may vary over time, it is better tooopt for relative script/file paths in hello `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="60c66-163">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="60c66-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="60c66-164">Merhaba ilk URI segmenti için dosyalar tutulur sonra yol bilgisi indirilen hello `fileUris` özellik listesi.</span><span class="sxs-lookup"><span data-stu-id="60c66-164">Path information after hello first URI segment is retained for files downloaded via hello `fileUris` property list.</span></span>  <span data-ttu-id="60c66-165">Merhaba aşağıdaki tabloda gösterildiği gibi indirilen dosyaları indirme alt dizinleri tooreflect hello yapısını hello eşlenmiş `fileUris` değerleri.</span><span class="sxs-lookup"><span data-stu-id="60c66-165">As shown in hello table below, downloaded files are mapped into download subdirectories tooreflect hello structure of hello `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="60c66-166">Karşıdan yüklenen dosyalar örnekleri</span><span class="sxs-lookup"><span data-stu-id="60c66-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="60c66-167">FileUris URI</span><span class="sxs-lookup"><span data-stu-id="60c66-167">URI in fileUris</span></span> | <span data-ttu-id="60c66-168">Göreli indirilen konumu</span><span class="sxs-lookup"><span data-stu-id="60c66-168">Relative downloaded location</span></span> | <span data-ttu-id="60c66-169">Mutlak konum indirilen *</span><span class="sxs-lookup"><span data-stu-id="60c66-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="60c66-170">\*Olarak yukarıdaki hello mutlak dizin yolları hello ömrü hello VM, ancak tek bir hello CustomScript uzantısını yürütülmesi içinde değil üzerinden değiştirir.</span><span class="sxs-lookup"><span data-stu-id="60c66-170">\* As above, hello absolute directory paths will change over hello lifetime of hello VM, but not within a single execution of hello CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="60c66-171">Destek</span><span class="sxs-lookup"><span data-stu-id="60c66-171">Support</span></span>

<span data-ttu-id="60c66-172">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz hello [MSDN Azure ve yığın taşması forumları] Azure uzmanlarıyla hello (https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="60c66-172">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="60c66-173">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="60c66-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="60c66-174">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin.</span><span class="sxs-lookup"><span data-stu-id="60c66-174">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="60c66-175">Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="60c66-175">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
