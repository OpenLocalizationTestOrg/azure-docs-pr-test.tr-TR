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
# <a name="custom-script-extension-for-windows"></a>Windows için özel betik uzantısı

Merhaba özel betik uzantısının indirir ve Azure sanal makinelerde komut dosyalarını çalıştırır. Bu dağıtım yapılandırmaları, yazılım yükleme veya başka bir yapılandırma için yararlı bir uzantısıdır / yönetim görevi. Komut dosyaları Azure depolama veya GitHub indirilen veya toohello çalışma zamanı uzantısı Azure portalında sağlanan. Merhaba özel betik uzantısı Azure Resource Manager şablonları ile tümleşir ve hello Azure CLI, PowerShell, Azure portal veya hello Azure sanal makine REST API'sini kullanarak da çalıştırılabilir.

Bu belge nasıl toouse hello özel betik uzantısı kullanılarak hello Azure PowerShell modülü, Azure Resource Manager şablonları ve sorun giderme adımları Windows sistemlerinde ayrıntıları ayrıntıları verilmektedir.

## <a name="prerequisites"></a>Ön koşullar

### <a name="operating-system"></a>İşletim Sistemi

Windows, Windows Server 2008 R2 karşı çalıştırılabilir için hello özel betik uzantısının 2012, 2012 R2 ve 2016 serbest bırakır.

### <a name="script-location"></a>Komut dosyası konumu

Merhaba komut dosyası Azure Blob Depolama veya başka bir konuma geçerli bir URL ile erişilebilir depolanan toobe gerekir.

### <a name="internet-connectivity"></a>Internet bağlantısı

Merhaba özel betik uzantısı için Windows hello hedef sanal makinenin bağlı toohello gerektirir Internet. 

## <a name="extension-schema"></a>Uzantı Şeması

Merhaba aşağıdaki JSON hello özel betik uzantısının hello şemasını gösterir. Merhaba uzantısı, bir komut dosyası konumuna (Azure Storage veya başka bir konuma geçerli bir URL ile) ve komut tooexecute gerektirir. Azure Storage hello komut dosyası kaynağı olarak kullanıyorsanız, bir Azure depolama hesabı adı ve hesap anahtarı gereklidir. Bu öğeler hassas verisi olarak kabul edilir ve hello uzantıları korumalı ayarını yapılandırma dosyasında belirtilen. Azure VM uzantısının korumalı ayarı veri şifrelenir ve yalnızca hello hedef sanal makineye şifresi.

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

### <a name="property-values"></a>Özellik değerleri

| Ad | Değer / örnek |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Yayımcı | Microsoft.Compute |
| type | Uzantıları |
| typeHandlerVersion | 1.9 |
| fileUris (örneğin) | https://RAW.githubusercontent.com/Microsoft/dotnet-Core-Sample-Templates/master/dotnet-Core-Music-Windows/scripts/Configure-Music-App.ps1 |
| commandToExecute (örneğin) | PowerShell - ExecutionPolicy Unrestricted - dosya yapılandırma-müzik-app.ps1 |
| storageAccountName (örneğin) | examplestorageacct |
| storageAccountKey (örneğin) | TmJK/1N3AbAZ3q / + hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg == |

**Not** -bu özellik adları büyük/küçük harfe duyarlıdır. Tooavoid dağıtım sorunlarını görüldüğü gibi Hello adları kullanın.

## <a name="template-deployment"></a>Şablon dağıtımı

Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir. Merhaba JSON şeması Hello önceki bölümde ayrıntılı bir Azure Resource Manager şablon dağıtımı sırasında bir Azure Resource Manager şablonu toorun hello özel betik uzantısı kullanılabilir. Özel betik uzantısının burada bulunabilir hello içeren bir örnek şablonunu [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>PowerShell dağıtım

Merhaba `Set-AzureRmVMCustomScriptExtension` komutu kullanılan tooadd hello özel betik uzantısı tooan varolan sanal makine olabilir. Daha fazla bilgi için bkz: [kümesi AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a>Sorun giderme ve Destek

### <a name="troubleshoot"></a>Sorun giderme

Veri uzantısı dağıtımları hello durumuyla ilgili hello Azure portal ve hello Azure PowerShell modülü kullanılarak alınabilir. toosee hello dağıtım durumu hello aşağıdaki komutu çalıştırın, belirli bir VM için uzantıları.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Uzantı yürütme hello altında bulunan oturum toofiles dizin hello hedef sanal makinede aşağıdaki çıktı.
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

Merhaba, dizin hello hedef sanal makinede aşağıdaki hello içine indirilen dosyaları belirtilen.
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
Burada `<n>` hangi hello uzantısı yürütmeleri arasında değişebilir ondalık bir tamsayıdır.  Merhaba `1.*` değerle hello gerçek, geçerli `typeHandlerVersion` hello uzantısı değeri.  Örneğin, hello gerçek dizin olabilir `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.  

Merhaba yürütülürken `commandToExecute` komutunu hello uzantısına ayarlayacak bu dizin (örneğin, `...\Downloads\2`) hello geçerli çalışma dizini olarak. İndirilen bu etkinleştirir hello kullan göreli yollar toolocate hello dosyaların hello `fileURIs` özelliği. Merhaba örnekler için aşağıdaki tabloya bakın.

Merhaba mutlak indirme yolunu zaman içinde değişebildiğinden hello yollarında göreli komut dosyası için daha iyi tooopt olan `commandToExecute` , mümkün olduğunda dize. Örneğin:
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

Merhaba ilk URI segmenti için dosyalar tutulur sonra yol bilgisi indirilen hello `fileUris` özellik listesi.  Merhaba aşağıdaki tabloda gösterildiği gibi indirilen dosyaları indirme alt dizinleri tooreflect hello yapısını hello eşlenmiş `fileUris` değerleri.  

#### <a name="examples-of-downloaded-files"></a>Karşıdan yüklenen dosyalar örnekleri

| FileUris URI | Göreli indirilen konumu | Mutlak konum indirilen * |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

\*Olarak yukarıdaki hello mutlak dizin yolları hello ömrü hello VM, ancak tek bir hello CustomScript uzantısını yürütülmesi içinde değil üzerinden değiştirir.

### <a name="support"></a>Destek

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz hello [MSDN Azure ve yığın taşması forumları] Azure uzmanlarıyla hello (https://azure.microsoft.com/en-us/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin. Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).
