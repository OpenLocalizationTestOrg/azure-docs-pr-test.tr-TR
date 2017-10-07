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
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a>Özel betik uzantısı hello Klasik dağıtım modeli kullanılarak Windows için

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Merhaba özel betik uzantısının indirir ve Azure sanal makinelerde komut dosyalarını çalıştırır. Bu dağıtım yapılandırmaları, yazılım yükleme veya başka bir yapılandırma için yararlı bir uzantısıdır / yönetim görevi. Komut dosyaları Azure depolama veya GitHub indirilen veya toohello çalışma zamanı uzantısı Azure portalında sağlanan. Merhaba özel betik uzantısı Azure Resource Manager şablonları ile tümleşir ve hello Azure CLI, PowerShell, Azure portal veya hello Azure sanal makine REST API'sini kullanarak da çalıştırılabilir.

Bu belge nasıl toouse hello özel betik uzantısı kullanılarak hello Azure PowerShell modülü, Azure Resource Manager şablonları ve sorun giderme adımları Windows sistemlerinde ayrıntıları ayrıntıları verilmektedir.

## <a name="prerequisites"></a>Ön koşullar

### <a name="operating-system"></a>İşletim Sistemi

Windows, Windows Server 2008 R2 karşı çalıştırılabilir için hello özel betik uzantısının 2012, 2012 R2 ve 2016 serbest bırakır.

### <a name="script-location"></a>Komut dosyası konumu

Merhaba komut dosyası Azure depolama veya başka bir konuma geçerli bir URL ile erişilebilir depolanan toobe gerekir.

### <a name="internet-connectivity"></a>Internet bağlantısı

Merhaba özel betik uzantısı için Windows hello hedef sanal makinenin bağlı toohello gerektirir Internet. 

## <a name="extension-schema"></a>Uzantı Şeması

Merhaba aşağıdaki JSON hello özel betik uzantısının hello şemasını gösterir. Merhaba uzantısı, bir komut dosyası konumuna (Azure Storage veya başka bir konuma geçerli bir URL ile) ve komut tooexecute gerektirir. Azure Storage hello komut dosyası kaynağı olarak kullanıyorsanız, bir Azure depolama hesabı adı ve hesap anahtarı gereklidir. Bu öğeler hassas verisi olarak kabul edilir ve hello uzantıları korumalı ayarını yapılandırma dosyasında belirtilen. Azure VM uzantısının korumalı ayarı veri şifrelenir ve yalnızca hello hedef sanal makineye şifresi.

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

### <a name="property-values"></a>Özellik değerleri

| Ad | Değer / örnek |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Yayımcı | Microsoft.Compute |
| Uzantısı | CustomScriptExtension |
| typeHandlerVersion | 1.8 |
| fileUris (örneğin) | https://RAW.githubusercontent.com/Microsoft/dotnet-Core-Sample-Templates/master/dotnet-Core-Music-Windows/scripts/Configure-Music-App.ps1 |
| commandToExecute (örneğin) | PowerShell - ExecutionPolicy Unrestricted - dosya yapılandırma-müzik-app.ps1 |

## <a name="template-deployment"></a>Şablon dağıtımı

Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir. Merhaba JSON şeması Hello önceki bölümde ayrıntılı bir Azure Resource Manager şablon dağıtımı sırasında bir Azure Resource Manager şablonu toorun hello özel betik uzantısı kullanılabilir. Özel betik uzantısının burada bulunabilir hello içeren bir örnek şablonunu [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>PowerShell dağıtım

Merhaba `Set-AzureVMCustomScriptExtension` komutu kullanılan tooadd hello özel betik uzantısı tooan varolan sanal makine olabilir. Daha fazla bilgi için bkz: [kümesi AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a>Sorun giderme ve Destek

### <a name="troubleshoot"></a>Sorun giderme

Veri uzantısı dağıtımları hello durumuyla ilgili hello Azure portal ve hello Azure PowerShell modülü kullanılarak alınabilir. toosee hello dağıtım durumu hello aşağıdaki komutu çalıştırın, belirli bir VM için uzantıları.

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Uzantı yürütme bize dizin hello hedef sanal makinede aşağıdaki hello bulunan oturum toofiles çıktı.

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

Merhaba komut dosyasının kendisini dizin hello hedef sanal makinede aşağıdaki hello içine yüklenir.

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a>Destek

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz hello Azure uzmanlarıyla hello [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin. Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).
