---
title: "Sanal makine uzantıları ile uygulama dağıtımı otomatikleştirme | Microsoft Docs"
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
ms.openlocfilehash: f2996eef71b39c6240fac5484854f72d3e657d0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Windows VM'ler için Azure Resource Manager şablonları ile uygulama dağıtımı

Tüm Azure infrastructural gereksinimleri belirledikten ve bir dağıtım şablonuna çevrilen sonra gerçek uygulama dağıtımı ele alınması gerekir. Uygulama dağıtımı burada gerçek uygulama ikili dosyaların Azure kaynaklarını üzerine yüklenmesi için başvuruyor. Müzik deposu örnek, .net Core ve IIS gereken yüklenmeli ve her sanal makine üzerinde yapılandırılmış. Müzik deposu ikili dosyasının sanal makineye yüklenmesi gerekmez ve müzik deposu veritabanı önceden oluşturulmuş.

Bu belge, uygulama dağıtımı ve yapılandırması Azure sanal makineler için sanal makine uzantıları nasıl otomatikleştirebilirsiniz ayrıntıları. Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır. En iyi deneyim için Azure aboneliği ve Azure Resource Manager şablonu ile birlikte çalışma çözümü örneği önceden dağıtın. Tam veri şablonunun burada – bulunabilir [müzik deposu dağıtım Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="configuration-script"></a>Yapılandırma komut dosyası
Sanal makine uzantıları yapılandırma Otomasyon sağlamak için sanal makinelere karşı yürütme özelleştirilmiş programlardır. Uzantıları, virüsten koruma, günlük yapılandırmasını ve Docker yapılandırması gibi birçok belirli amaçlar için kullanılabilir. Özel betik uzantısı, bir sanal makine herhangi komut dosyasını çalıştırmak için kullanılabilir. Müzik deposu örneği ile Windows sanal makineleri yapılandırmak ve müzik mağaza uygulamasını yüklemek için özel betik uzantısı kadar değil.

Sanal makine uzantıları bir Azure Resource Manager şablonu nasıl bildirilir ayrıntılı önce çalıştırılan komut dosyasını inceleyin. Bu komut dosyası müzik mağaza uygulamasını barındırmak için Windows sanal makine yapılandırır. Çalıştırdığınızda, betik tüm yazılım, müzik deposu uygulama kaynak denetiminden yükleyin ve veritabanını hazırlama yükler. 

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
VM uzantıları bir sanal makine uzantısı kaynak Azure Resource Manager şablonunda ekleyerek derleme zamanında çalıştırılabilir. Uzantı, Visual Studio kaynak Ekleme Sihirbazı'nı ya da geçerli JSON şablonuna ekleyerek eklenebilir. Betik uzantısı kaynak sanal makine kaynağı içinde iç içe yerleştirilmiş; Bu aşağıdaki örnekte görülebilir.

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [VM betik uzantısı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339). 

Fark aşağıda JSON betiği Github'da depolanır. Bu komut dosyası ayrıca Azure Blob Depolama alanında depolanabilir. Ayrıca, Azure Resource Manager şablonları şablonu parametrelerinin değerlerini komut dosyası yürütme için parametre olarak kullanılabilir olduğunu oluşturulması için komut dosyası yürütme dizesi izin verin. Bu durumda veri şablonları dağıtırken sağlanır ve bu değerler, daha sonra komut dosyasını yürütürken kullanılabilir.

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

Yukarıda belirtildiği gibi ayrıca Azure Blob depolama alanına özel komut dosyalarınızı depolamak mümkündür. Komut dosyası kaynakları blob storage'da depolamak için iki seçenek vardır; kapsayıcı/komut dosyası ya da ortak yapın ve aynı olarak yukarıdaki yaklaşımını izleyin veya Ayrıca storageAccountName ve storageAccountKey CustomScriptExtension kaynak tanımı belirtmesini gerektiren özel blob depolamada tutulabilir.

Aşağıdaki örnekte biz bir adım daha fazla gitti. Depolama hesabı adı ve anahtar dağıtımı sırasında bir parametre veya değişken sağlamak mümkün olsa da, Resource Manager şablonları sağlamak `listKeys` depolama hesabı anahtarı programlı olarak alabilir ve şablona IT işlevi Dağıtım zamanında.

CustomScriptExtension kaynak tanımı aşağıdaki örnekte, özel bir komut dosyası zaten adlı bir Azure depolama hesabı yüklendi `mystorageaccount9999` olarak adlandırılan, başka bir kaynak grubunda var `mysa999rgname`. Biz bu kaynak içeren bir şablonu dağıttığınızda `listKeys` işlevi program aracılığıyla depolama hesabı için depolama hesabı anahtarı edinir `mystorageaccount9999` kaynak grubunda `mysa999rgname` ve şablona bize içinde ekler.

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

Bu yaklaşımın ana avantajı, şablon veya dağıtım parametrelerinizi depolama hesabı anahtar durumunda değiştirmek için gerektirmediğinden emin olur.

Özel betik uzantısı kullanma hakkında daha fazla bilgi için bkz: [özel betik uzantılarının Resource Manager şablonları ile](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-step"></a>Sonraki adım
<hr>

[Daha fazla Azure Resource Manager şablonları keşfedin](https://github.com/Azure/azure-quickstart-templates)

