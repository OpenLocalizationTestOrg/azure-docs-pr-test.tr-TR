---
title: "aaaAutomating sanal makine uzantıları ile uygulama dağıtımı | Microsoft Docs"
description: "Azure sanal makinesi DotNet çekirdek Öğreticisi"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="6ba17-103">Windows VM'ler için Azure Resource Manager şablonları ile uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="6ba17-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="6ba17-104">Tüm Azure infrastructural gereksinimleri belirledikten ve bir dağıtım şablonuna çevrilen sonra hello gerçek uygulama dağıtımı ele toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ba17-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="6ba17-105">Uygulama dağıtımı burada tooinstalling hello gerçek uygulama ikililerini Azure kaynaklarını üzerine başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="6ba17-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="6ba17-106">Merhaba müzik deposu örnek, .net için çekirdek ve IIS yüklü ve her sanal makinede yapılandırılan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ba17-106">For hello Music Store sample, .Net Core and IIS need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="6ba17-107">Merhaba müzik deposu ikili dosyaları hello sanal makineye yüklenmesi yüklü toobe gerekir ve hello müzik deposu veritabanı önceden oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="6ba17-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="6ba17-108">Bu belge, sanal makine uzantıları uygulama dağıtımı ve yapılandırması tooAzure sanal makineleri nasıl otomatikleştirebilirsiniz ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="6ba17-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="6ba17-109">Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="6ba17-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="6ba17-110">Merhaba en iyi deneyim için önceden hello çözüm tooyour Azure aboneliği ve hello Azure Resource Manager şablonu ile birlikte çalışma örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6ba17-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="6ba17-111">Merhaba tam şablon burada – bulunabilir [müzik deposu dağıtım Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="6ba17-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="6ba17-112">Yapılandırma komut dosyası</span><span class="sxs-lookup"><span data-stu-id="6ba17-112">Configuration script</span></span>
<span data-ttu-id="6ba17-113">Sanal makine, sanal makineleri tooprovide yapılandırma Otomasyon karşı yürütme özel programları uzantılarıdır.</span><span class="sxs-lookup"><span data-stu-id="6ba17-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="6ba17-114">Uzantıları, virüsten koruma, günlük yapılandırmasını ve Docker yapılandırması gibi birçok belirli amaçlar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ba17-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="6ba17-115">Merhaba özel betik uzantısı herhangi bir sanal makine komut dosyası kullanılan toorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="6ba17-115">hello Custom Script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="6ba17-116">Merhaba müzik deposu örnekle bu toohello özel betik uzantısı tooconfigure hello Windows sanal makineleri ve hello müzik deposu uygulamayı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6ba17-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Windows virtual machines and install hello Music Store application.</span></span>

<span data-ttu-id="6ba17-117">Sanal makine uzantıları bir Azure Resource Manager şablonu nasıl bildirilir ayrıntılı önce çalıştırılır hello komut dosyasını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="6ba17-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="6ba17-118">Bu komut dosyası hello Windows sanal makine toohost hello müzik deposu uygulama yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="6ba17-118">This script configures hello Windows virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="6ba17-119">Çalıştırdığınızda, tüm gerekli yazılım hello betik yükler kaynak denetiminden hello müzik deposu uygulamayı yükleyip hello veritabanı hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="6ba17-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

> <span data-ttu-id="6ba17-120">Bu örnek tanıtım amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6ba17-120">This sample is for demonstration purposes.</span></span>

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a><span data-ttu-id="6ba17-121">VM betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="6ba17-121">VM Script Extension</span></span>
<span data-ttu-id="6ba17-122">VM uzantıları bir sanal makine hello Azure Resource Manager şablonunda hello uzantısı kaynak ekleyerek derleme zamanında çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ba17-122">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="6ba17-123">Merhaba uzantısı hello Visual Studio kaynak Ekleme Sihirbazı'nı ya da geçerli JSON hello şablonuna ekleyerek eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="6ba17-123">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="6ba17-124">Merhaba betik uzantısı kaynak sanal makine kaynağı hello içinde iç içe yerleştirilmiş; Bu örnekte aşağıdaki hello görülebilir.</span><span class="sxs-lookup"><span data-stu-id="6ba17-124">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="6ba17-125">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [VM betik uzantısı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="6ba17-125">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="6ba17-126">Merhaba aşağıdaki betik hello JSON Github'da depolanan dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6ba17-126">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="6ba17-127">Bu komut dosyası ayrıca Azure Blob Depolama alanında depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="6ba17-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="6ba17-128">Ayrıca, Azure Resource Manager şablonları hello komut dosyası yürütme dize toobe şablonu parametrelerinin değerlerini komut dosyası yürütme için parametre olarak kullanılabilir olacağı şekilde oluşturulan izin verin.</span><span class="sxs-lookup"><span data-stu-id="6ba17-128">Also, Azure Resource Manager templates allow hello script execution string toobe constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="6ba17-129">Bu durumda veri hello şablonları dağıtırken sağlanır ve bu değerler, daha sonra hello komut dosyası yürütülürken kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ba17-129">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="6ba17-130">Yukarıda belirtildiği gibi Azure Blob depolama alanına özel komut dosyaları olası toostore de olabilir.</span><span class="sxs-lookup"><span data-stu-id="6ba17-130">As mentioned above, it is also possible toostore your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="6ba17-131">Blob depolama alanına hello komut dosyası kaynakları depolamak için iki seçenek vardır; kapsayıcı/komut dosyası ortak hello ve aynı yukarıdaki yaklaşımını hello izleyin olun ya da aynı zamanda tooprovide hello storageAccountName ve storageAccountKey toohello CustomScriptExtension kaynak tanımı gerektiren özel blob depolama alanına tutulabilir.</span><span class="sxs-lookup"><span data-stu-id="6ba17-131">There are two options for storing hello script resources in blob storage; either make hello container/script public and follow hello same approach as above, or it can also be kept in private blob storage which requires you tooprovide hello storageAccountName and storageAccountKey toohello CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="6ba17-132">Merhaba aşağıdaki örnekte biz bir adım daha fazla gitti.</span><span class="sxs-lookup"><span data-stu-id="6ba17-132">In hello example below we have gone a step further.</span></span> <span data-ttu-id="6ba17-133">Bu olası tooprovide hello depolama hesabı adı ve anahtar bir parametre veya değişken dağıtımı sırasında olsa da, Resource Manager şablonları hello sağlamak `listKeys` hello depolama hesabı edinebilirsiniz işlevi program aracılığıyla anahtarı ve toohello Ekle Dağıtım zamanında şablonu sizin için.</span><span class="sxs-lookup"><span data-stu-id="6ba17-133">While it is possible tooprovide hello storage account name and key as a parameter or variable during deployment, Resource Manager templates provide hello `listKeys` function that can obtain hello storage account key programmatically and insert it in toohello template for you at deployment time.</span></span>

<span data-ttu-id="6ba17-134">Azure depolama hesabı CustomScriptExtension kaynak tanımı aşağıdaki bizim özel bir komut dosyası karşıya yüklenen tooan zaten hello örnekte adlı `mystorageaccount9999` olarak adlandırılan, başka bir kaynak grubunda var `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="6ba17-134">In hello example CustomScriptExtension resource definition below, our custom script has already been uploaded tooan Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="6ba17-135">Biz bu kaynak içeren bir şablonu dağıttığınızda, hello `listKeys` işlevi program aracılığıyla hello depolama hesabının hello depolama hesabı anahtarı edinir `mystorageaccount9999` hello kaynak grubu içinde `mysa999rgname` ve bize toohello şablonunda ekler.</span><span class="sxs-lookup"><span data-stu-id="6ba17-135">When we deploy a template containing this resource, hello `listKeys` function programmatically obtains hello storage account key for hello storage account `mystorageaccount9999` in hello Resource Group `mysa999rgname` and inserts it in toohello template for us.</span></span>

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
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

<span data-ttu-id="6ba17-136">Bu yaklaşımın Hello ana avantajı, toochange şablonunuzu gerektirmez veya depolama hesabı anahtarı değiştirerek dağıtım parametrelerini hello olayı içinde hello değil.</span><span class="sxs-lookup"><span data-stu-id="6ba17-136">hello main benefit of this approach is that it does not require you toochange your template or deployment parameters in hello event of hello storage account key changing.</span></span>

<span data-ttu-id="6ba17-137">Merhaba özel betik uzantısı kullanma hakkında daha fazla bilgi için bkz: [özel betik uzantılarının Resource Manager şablonları ile](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6ba17-137">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="6ba17-138">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="6ba17-138">Next Step</span></span>
<hr>

[<span data-ttu-id="6ba17-139">Daha fazla Azure Resource Manager şablonları keşfedin</span><span class="sxs-lookup"><span data-stu-id="6ba17-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

