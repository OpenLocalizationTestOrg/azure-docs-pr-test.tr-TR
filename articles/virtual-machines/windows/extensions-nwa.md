---
title: "Windows için Ağ İzleyicisi Aracısı sanal makine uzantısı aaaAzure | Microsoft Docs"
description: "Bir sanal makine uzantısını kullanarak Windows sanal makine üzerinde Ağ İzleyicisi Aracısı Hello dağıtın."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a>Windows için Ağ İzleyicisi Aracısı sanal makine uzantısı

## <a name="overview"></a>Genel Bakış

[Azure Ağ İzleyicisi](https://review.docs.microsoft.com/en-us/azure/network-watcher/) Azure ağları için izleme sağlayan bir ağ performans izleme, tanılama ve analiz hizmetidir. Ağ İzleyicisi Aracısı sanal makine uzantısı Hello Azure sanal makinelerde hello Ağ İzleyicisi özelliklerinden bazıları için gerekli değildir. Bu, isteğe bağlı ve diğer gelişmiş işlevler üzerindeki ağ trafiğini yakalama içerir.

Bu belge ayrıntıları hello platformları ve dağıtım seçenekleri için Windows hello Ağ İzleyicisi Aracısı sanal makine uzantısı için desteklenmiyor.

## <a name="prerequisites"></a>Ön koşullar

### <a name="operating-system"></a>İşletim sistemi

Windows, Windows Server 2008 R2 karşı çalıştırılabilir için hello Ağ İzleyicisi Aracısı uzantısı 2012, 2012 R2 ve 2016 serbest bırakır. Nano Server hello Not şu anda desteklenmiyor.

### <a name="internet-connectivity"></a>İnternet bağlantısı

Merhaba Ağ İzleyicisi Aracısı işlevleri bazıları hello hedef sanal makinenin bağlı toohello Internet olması gerekir. Merhaba özelliği tooestablish giden bağlantılar hello Ağ İzleyicisi Aracısı özelliklerden bazıları düzgün çalışmamasına veya kullanılamaz hale. Daha fazla ayrıntı için lütfen bkz hello [Ağ İzleyicisi belgeleri](../../network-watcher/network-watcher-monitoring-overview.md).

## <a name="extension-schema"></a>Uzantı Şeması

Merhaba aşağıdaki JSON hello Ağ İzleyicisi Aracısı uzantısı için hello şema gösterir. Merhaba uzantısı ne gerektirir ya da şu anda herhangi bir kullanıcı tarafından sağlanan ayarını destekler ve kendi varsayılan yapılandırmasına dayanır.

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a>Özellik değerleri

| Ad | Değer / örnek |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Yayımcı | Microsoft.Azure.NetworkWatcher |
| type | NetworkWatcherAgentWindows |
| typeHandlerVersion | 1.4 |


## <a name="template-deployment"></a>Şablon dağıtımı

Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir. Merhaba JSON şeması Hello önceki bölümde ayrıntılı bir Azure Resource Manager şablon dağıtımı sırasında bir Azure Resource Manager şablonu toorun hello Ağ İzleyicisi Aracısı uzantısı kullanılabilir.

## <a name="powershell-deployment"></a>PowerShell dağıtım

Merhaba `Set-AzureRmVMExtension` komutu kullanılan toodeploy hello Ağ İzleyicisi Aracısı sanal makine uzantısı tooan varolan sanal makine olabilir.

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a>Sorun giderme ve destek

### <a name="troubleshooting"></a>Sorun giderme

Veri uzantısı dağıtımları hello durumuyla ilgili hello Azure portal ve hello Azure PowerShell modülü kullanılarak alınabilir. Aşağıdaki komutu kullanarak çalışma hello belirli bir VM için uzantıların toosee hello dağıtım durumu hello Azure PowerShell modülü.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

Uzantı yürütme hello bulunan oturum toofiles directory aşağıdaki çıktı:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a>Destek

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, toohello Ağ İzleyicisi kullanıcı kılavuzu belgelerine başvurun veya hello Azure başvurun hello uzmanlarıyla [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin. Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).
