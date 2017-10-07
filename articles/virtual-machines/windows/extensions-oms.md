---
title: "Windows için Azure sanal makine uzantısı aaaOMS | Microsoft Docs"
description: "Merhaba OMS Aracısı'nı kullanarak bir sanal makine uzantısı Windows sanal makine dağıtın."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a>Windows için OMS sanal makine uzantısı

Operations Management Suite (OMS) bulut izleme, uyarma ve uyarı düzeltme özellikleri sağlar ve şirket içi varlıklar. Merhaba OMS Aracısı sanal makine uzantısı Windows için yayımlanan ve Microsoft tarafından desteklenmiyor. Merhaba uzantısı Azure sanal makinelerde hello OMS Aracısı'nı yükler ve sanal makineleri olan bir OMS çalışma kaydeder. Bu belge ayrıntıları hello platformları, yapılandırmaları ve dağıtım seçenekleri için Windows hello OMS sanal makine uzantısı için desteklenmiyor.

## <a name="prerequisites"></a>Ön koşullar

### <a name="operating-system"></a>İşletim sistemi
Windows, Windows Server 2008 R2 karşı çalıştırılabilir için hello OMS Aracısı uzantısı 2012, 2012 R2 ve 2016 serbest bırakır.

### <a name="internet-connectivity"></a>İnternet bağlantısı
OMS Aracısı uzantısı için Windows Hello gerektirir hello hedef sanal makinenin bağlı toohello Internet. 

## <a name="extension-schema"></a>Uzantı Şeması

Merhaba aşağıdaki JSON hello OMS Aracısı uzantısı için hello şema gösterir. Merhaba uzantısı hello hedef OMS çalışma alanından hello çalışma alanı kimliği ve çalışma alanı anahtarı gerekiyor, bunlar hello OMS portalında bulunabilir. Merhaba çalışma alanı anahtarı hassas verileri olarak değerlendirilmesi için bir korumalı ayarı yapılandırmasında depolanması gerekir. Azure VM uzantısının korumalı ayarı veri şifrelenir ve yalnızca hello hedef sanal makineye şifresi. Unutmayın **Workspaceıd** ve **workspaceKey** büyük küçük harfe duyarlıdır.

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a>Özellik değerleri

| Ad | Değer / örnek |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Yayımcı | Microsoft.EnterpriseCloud.Monitoring |
| type | MicrosoftMonitoringAgent |
| typeHandlerVersion | 1.0 |
| Workspaceıd (örneğin) | 6f680a37-00c6-41C7-a93f-1437e3462574 |
| workspaceKey (örneğin) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ == |

## <a name="template-deployment"></a>Şablon dağıtımı

Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir. Merhaba JSON şeması Hello önceki bölümde ayrıntılı bir Azure Resource Manager şablon dağıtımı sırasında bir Azure Resource Manager şablonu toorun hello OMS Aracısı uzantısı kullanılabilir. Merhaba OMS Aracısı VM uzantısı içeren bir örnek şablonu hello üzerinde bulunabilir [Azure hızlı başlangıç Galerisi](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm). 

Hello JSON bir sanal makine uzantısı hello sanal makine kaynağı içinde iç içe geçmiş veya hello kök veya Resource Manager JSON şablonu en üst düzeyinde yerleştirilir. Merhaba JSON Hello yerleşimini hello değeri hello kaynak adı ve türü etkiler. Daha fazla bilgi için bkz: [Ayarla alt kaynakları için ad ve tür](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Merhaba aşağıdaki örneği hello OMS uzantısı hello sanal makine kaynağı içinde iç içe geçmiş varsayar. Merhaba uzantısı kaynak iç içe geçirme sırasında hello JSON hello yerleştirilir `"resources": []` hello sanal makinenin nesnesi.


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

Merhaba uzantısı JSON hello hello şablon kökünde yerleştirirken başvuru toohello üst sanal makinesini hello kaynak adı içerir ve hello türü hello iç içe geçmiş yapılandırma yansıtır. 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a>PowerShell dağıtım

Merhaba `Set-AzureRmVMExtension` komutu kullanılan toodeploy hello OMS Aracısı sanal makine uzantısı tooan varolan sanal makine olabilir. Hello komutu çalıştırmadan önce bir PowerShell karma tablosu toobe hello ortak ve özel yapılandırmaları gerekir. 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a>Sorun giderme ve Destek

### <a name="troubleshoot"></a>Sorun giderme

Veri uzantısı dağıtımları hello durumuyla ilgili hello Azure portal ve hello Azure PowerShell modülü kullanılarak alınabilir. Aşağıdaki komutu kullanarak çalışma hello belirli bir VM için uzantıların toosee hello dağıtım durumu hello Azure PowerShell modülü.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Uzantı yürütme hello bulunan oturum toofiles directory aşağıdaki çıktı:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a>Destek

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz hello Azure uzmanlarıyla hello [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin. Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).
