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
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Windows VM'ler için Azure Resource Manager şablonları ile uygulama dağıtımı

Tüm Azure infrastructural gereksinimleri belirledikten ve bir dağıtım şablonuna çevrilen sonra hello gerçek uygulama dağıtımı ele toobe gerekir. Uygulama dağıtımı burada tooinstalling hello gerçek uygulama ikililerini Azure kaynaklarını üzerine başvuruyor. Merhaba müzik deposu örnek, .net için çekirdek ve IIS yüklü ve her sanal makinede yapılandırılan toobe gerekir. Merhaba müzik deposu ikili dosyaları hello sanal makineye yüklenmesi yüklü toobe gerekir ve hello müzik deposu veritabanı önceden oluşturulmuş.

Bu belge, sanal makine uzantıları uygulama dağıtımı ve yapılandırması tooAzure sanal makineleri nasıl otomatikleştirebilirsiniz ayrıntıları. Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır. Merhaba en iyi deneyim için önceden hello çözüm tooyour Azure aboneliği ve hello Azure Resource Manager şablonu ile birlikte çalışma örneği dağıtın. Merhaba tam şablon burada – bulunabilir [müzik deposu dağıtım Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="configuration-script"></a>Yapılandırma komut dosyası
Sanal makine, sanal makineleri tooprovide yapılandırma Otomasyon karşı yürütme özel programları uzantılarıdır. Uzantıları, virüsten koruma, günlük yapılandırmasını ve Docker yapılandırması gibi birçok belirli amaçlar için kullanılabilir. Merhaba özel betik uzantısı herhangi bir sanal makine komut dosyası kullanılan toorun olabilir. Merhaba müzik deposu örnekle bu toohello özel betik uzantısı tooconfigure hello Windows sanal makineleri ve hello müzik deposu uygulamayı yükleyin.

Sanal makine uzantıları bir Azure Resource Manager şablonu nasıl bildirilir ayrıntılı önce çalıştırılır hello komut dosyasını inceleyin. Bu komut dosyası hello Windows sanal makine toohost hello müzik deposu uygulama yapılandırır. Çalıştırdığınızda, tüm gerekli yazılım hello betik yükler kaynak denetiminden hello müzik deposu uygulamayı yükleyip hello veritabanı hazırlayın. 

> Bu örnek tanıtım amacıyla kullanılır.

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

## <a name="vm-script-extension"></a>VM betik uzantısı
VM uzantıları bir sanal makine hello Azure Resource Manager şablonunda hello uzantısı kaynak ekleyerek derleme zamanında çalıştırılabilir. Merhaba uzantısı hello Visual Studio kaynak Ekleme Sihirbazı'nı ya da geçerli JSON hello şablonuna ekleyerek eklenebilir. Merhaba betik uzantısı kaynak sanal makine kaynağı hello içinde iç içe yerleştirilmiş; Bu örnekte aşağıdaki hello görülebilir.

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [VM betik uzantısı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339). 

Merhaba aşağıdaki betik hello JSON Github'da depolanan dikkat edin. Bu komut dosyası ayrıca Azure Blob Depolama alanında depolanabilir. Ayrıca, Azure Resource Manager şablonları hello komut dosyası yürütme dize toobe şablonu parametrelerinin değerlerini komut dosyası yürütme için parametre olarak kullanılabilir olacağı şekilde oluşturulan izin verin. Bu durumda veri hello şablonları dağıtırken sağlanır ve bu değerler, daha sonra hello komut dosyası yürütülürken kullanılabilir.

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

Yukarıda belirtildiği gibi Azure Blob depolama alanına özel komut dosyaları olası toostore de olabilir. Blob depolama alanına hello komut dosyası kaynakları depolamak için iki seçenek vardır; kapsayıcı/komut dosyası ortak hello ve aynı yukarıdaki yaklaşımını hello izleyin olun ya da aynı zamanda tooprovide hello storageAccountName ve storageAccountKey toohello CustomScriptExtension kaynak tanımı gerektiren özel blob depolama alanına tutulabilir.

Merhaba aşağıdaki örnekte biz bir adım daha fazla gitti. Bu olası tooprovide hello depolama hesabı adı ve anahtar bir parametre veya değişken dağıtımı sırasında olsa da, Resource Manager şablonları hello sağlamak `listKeys` hello depolama hesabı edinebilirsiniz işlevi program aracılığıyla anahtarı ve toohello Ekle Dağıtım zamanında şablonu sizin için.

Azure depolama hesabı CustomScriptExtension kaynak tanımı aşağıdaki bizim özel bir komut dosyası karşıya yüklenen tooan zaten hello örnekte adlı `mystorageaccount9999` olarak adlandırılan, başka bir kaynak grubunda var `mysa999rgname`. Biz bu kaynak içeren bir şablonu dağıttığınızda, hello `listKeys` işlevi program aracılığıyla hello depolama hesabının hello depolama hesabı anahtarı edinir `mystorageaccount9999` hello kaynak grubu içinde `mysa999rgname` ve bize toohello şablonunda ekler.

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

Bu yaklaşımın Hello ana avantajı, toochange şablonunuzu gerektirmez veya depolama hesabı anahtarı değiştirerek dağıtım parametrelerini hello olayı içinde hello değil.

Merhaba özel betik uzantısı kullanma hakkında daha fazla bilgi için bkz: [özel betik uzantılarının Resource Manager şablonları ile](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-step"></a>Sonraki adım
<hr>

[Daha fazla Azure Resource Manager şablonları keşfedin](https://github.com/Azure/azure-quickstart-templates)

