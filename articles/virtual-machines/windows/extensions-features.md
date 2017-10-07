---
title: "Windows Azure için aaaVirtual makine uzantıları ve özellikleri | Microsoft Docs"
description: "Hangi uzantıları ne bunlar sağlayın veya geliştirmek tarafından gruplandırılmış Azure sanal makineler için kullanılabilir olduğunu öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a>Sanal makine uzantıları ve özellikleri Windows için

Azure sanal makine uzantıları Azure sanal makinelerde dağıtım sonrası yapılandırma ve Otomasyon görevlerini sağlayan küçük uygulamalardır. Örneğin, bir sanal makineye yazılım yükleme, virüsten koruma veya Docker yapılandırma gerektiriyorsa, VM uzantısı için kullanılan toocomplete bu görevleri olabilir. Azure VM uzantıları ve Azure portal hello hello Azure CLI, PowerShell, Azure Resource Manager şablonları kullanarak çalıştırabilirsiniz. Uzantıları ile yeni bir sanal makine dağıtımı paketlenebilir veya varolan bir sistemle bağlantılı çalıştırın.

Bu belge, sanal makine uzantıları, sanal makine uzantıları ve Kılavuzu nasıl toodetect, yönetme ve sanal makine uzantıları kaldırma üzerinde kullanma önkoşulları genel bir bakış sağlar. Birçok VM uzantıları bulunduğundan, bu belgede genelleştirilmiş bilgiler sağlanmaktadır her potansiyel olarak benzersiz bir yapılandırmaya sahip. Uzantı özel ayrıntıları her belge belirli toohello tek tek uzantısı'nda bulunabilir.

## <a name="use-cases-and-samples"></a>Kullanım örnekleri ve örnekler

Birçok farklı Azure VM uzantıları vardır, her biri belirli bir kullanım örneği. Bazı örnek kullanım örnekleri şunlardır:

- PowerShell istenen durum yapılandırması tooa sanal makine için Windows hello DSC uzantısı kullanılarak uygulanır. Daha fazla bilgi için bkz: [Azure istenen durum yapılandırması uzantısı](extensions-dsc-overview.md).
- Sanal makine hello Microsoft İzleme Aracısı VM uzantısı kullanarak izlemeyi yapılandırın. Daha fazla bilgi için bkz: [bağlanmak Azure sanal makineleri tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).
- Azure altyapınızın hello Datadog uzantısı ile izlemeyi yapılandırma. Daha fazla bilgi için bkz: Merhaba [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Bir Azure sanal makinesi Chef kullanarak yapılandırın. Daha fazla bilgi için bkz: [otomatikleştirme Azure sanal makine dağıtımı Chef ile](chef-automation.md).

Ayrıca tooprocess özgü uzantılar, özel betik uzantısı hem Windows hem de Linux sanal makineler için kullanılabilir. Merhaba özel betik uzantısı Windows için bir sanal makine üzerinde çalışan bir PowerShell komut dosyası toobe sağlar. Yerel hangi Azure araçlar sağlayabilir ötesinde yapılandırma gerektiren Azure dağıtımları tasarlarken kullanışlıdır. Daha fazla bilgi için bkz: [Windows VM özel betik uzantısı](extensions-customscript.md).


## <a name="prerequisites"></a>Ön koşullar

Her sanal makine uzantısı önkoşulları kendi kümesine sahip. Örneği için bir önkoşul desteklenen Linux dağıtım hello Docker VM uzantısı vardır. Tek tek uzantıların gereksinimlerini hello uzantıya özgü belgelerinde açıklanmıştır.

### <a name="azure-vm-agent"></a>Azure VM aracısı
Hello Azure VM Aracısı bir Azure sanal makinesi ve hello Azure yapı denetleyicisi arasındaki etkileşimi yönetir. Merhaba VM Aracısı dağıtma ve yönetme Azure sanal makineler, çalışan VM uzantıları dahil olmak üzere birçok işlevsel görünüşlere için sorumludur. Hello Azure VM Aracısı Azure Marketi görüntülerinde önceden yüklenmiş ve desteklenen işletim sistemlerine yüklenebilir.

Desteklenen işletim sistemleri ve yükleme yönergeleri hakkında daha fazla bilgi için bkz: [Azure sanal makine Aracısı](agent-user-guide.md).

## <a name="discover-vm-extensions"></a>VM uzantıları Bul
Birçok farklı VM uzantıları, Azure sanal makineler ile kullanmak için kullanılabilir. tam bir listesi, toosee komutu hello Azure Resource Manager PowerShell modülü ile aşağıdaki hello çalıştırın. Bu komutu çalıştırdığınızda toospecify istenen hello konumu emin olun.

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a>VM uzantıları çalıştırın

Azure sanal makine uzantıları toomake yapılandırma değişiklikleri gerekir ya da bağlantı zaten dağıtılmış bir VM'de kurtarmak gerektiğinde faydalı olan mevcut sanal makinelerde çalıştırılabilir. VM uzantıları, Azure Resource Manager şablonu dağıtımlarında da gönderilebilir. Resource Manager şablonları ile uzantıları kullanarak dağıtılır ve dağıtım sonrası araya hello gerek kalmadan yapılandırılmış Azure sanal makineleri toobe etkinleştirebilirsiniz.

yöntemler aşağıdaki hello kullanılan toorun uzantı var olan bir sanal makineye karşı olabilir.

### <a name="powershell"></a>PowerShell

Birkaç PowerShell komutları tek tek uzantıların çalıştırmak için mevcut. bir liste toosee hello aşağıdaki PowerShell komutlarını çalıştırın.

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

Bu çıktı benzer toohello aşağıdakileri sağlar:

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

Merhaba aşağıdaki örnek hello özel betik uzantısı toodownload bir komut dosyası hello hedef sanal makine üzerine GitHub deposunu kullanır ve hello betiğini çalıştırın. Merhaba özel betik uzantısı ile ilgili daha fazla bilgi için bkz: [özel betik uzantısı genel bakış](extensions-customscript.md).

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

Bu örnekte, hello VM erişim uzantısı kullanılan tooreset hello yönetimsel bir Windows sanal makinenin paroladır. Merhaba VM erişim uzantısı ile ilgili daha fazla bilgi için bkz: [Windows VM Uzak Masaüstü'nü Sıfırla Hizmeti'nde](reset-rdp.md).

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

Merhaba `Set-AzureRmVMExtension` komutu kullanılan toostart tüm VM uzantısı olabilir. Daha fazla bilgi için bkz: Merhaba [kümesi AzureRmVMExtension başvuru](https://msdn.microsoft.com/en-us/library/mt603745.aspx).


### <a name="azure-portal"></a>Azure portalına

VM uzantısı hello Azure portal aracılığıyla uygulanan tooan varolan sanal makine olabilir. toodo, bu nedenle, hello sanal makine seçin toouse istiyorsanız, seçin **uzantıları**, tıklatıp **Ekle**. Bu, kullanılabilir uzantıları listesini sağlar. Merhaba istediğiniz ve hello hello Sihirbazı'ndaki adımları seçin.

Merhaba aşağıdaki görüntüde hello hello Azure portal Microsoft Antimalware uzantı hello yüklemesini gösterir.

![Kötü amaçlı yazılımdan koruma uzantısını yükleyin](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a>Azure Resource Manager şablonları

VM uzantıları eklenen tooan Azure Resource Manager şablonu olabilir ve hello şablon hello dağıtımı ile yürütüldü. Bir şablonla uzantıları tam olarak yapılandırılmış Azure dağıtımları oluşturmak için kullanışlıdır. Örneğin, aşağıdaki JSON yük dengeli sanal makineler ve Azure SQL veritabanını kümesi dağıtır ve ardından her VM .NET Core uygulama yükleyen bir Resource Manager şablonu alınırlar hello. Merhaba VM uzantısı hello yazılım yüklemesini mvc'deki.

Daha fazla bilgi için bkz: Merhaba [tam Resource Manager şablonu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

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

Daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma Windows VM uzantıları ile](template-description.md#extensions).

## <a name="secure-vm-extension-data"></a>VM uzantısı verileri güvenli

VM uzantısı çalıştırırken kimlik bilgilerini, depolama hesabı adları ve depolama hesabı erişim anahtarlarını gibi hassas bilgileri gerekli tooinclude olabilir. Birçok VM uzantıları verileri şifreler ve yalnızca hello hedef sanal makine içinde şifresini çözer korumalı bir yapılandırmayı içerir. Her bir uzantı uzantıya özgü belgelerinde ayrıntılı bir belirli korumalı yapılandırma şeması vardır.

Aşağıdaki örneğine hello için Windows hello özel betik uzantısı örneğini gösterir. Bu hello komutu tooexecute kimlik bilgileri kümesi içerir dikkat edin. Bu örnekte, hello komutu tooexecute şifrelenmez.


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
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Merhaba taşıyarak Hello yürütme dize güvenli **komutu tooexecute** özelliği toohello **korumalı** yapılandırma.

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

## <a name="troubleshoot-vm-extensions"></a>VM uzantıları sorun giderme

Her VM uzantısı özel sorun giderme adımları olabilir. Örneğin, hello özel betik uzantısı kullanırken, komut dosyası yürütme ayrıntılarını yerel olarak hello uzantısı çalıştırıldığı hello sanal makine üzerinde bulunabilir. Uzantı özel sorun giderme işlemleri uzantıya özgü belgelerinde açıklanmıştır.

Aşağıdaki sorun giderme adımları hello tooall sanal makine uzantıları uygulayın.

### <a name="view-extension-status"></a>Uzantı durumunu görüntüle

Bir sanal makine uzantısı bir sanal makine çalıştırdıktan sonra aşağıdaki PowerShell komut tooreturn uzantı durumunu hello kullanın. Örnek parametre adları kendi değerlerinizle değiştirin. Merhaba `Name` parametresi toohello uzantısı yürütme sırasında verilen hello adı alır.

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Merhaba çıktı hello aşağıdaki gibi görünür:

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

Uzantı yürütme durumu da hello Azure portalında bulunabilir. tooview hello durumu select hello sanal makine, bir uzantı seçin **uzantıları**, ve hello istenen uzantı seçin.

### <a name="rerun-vm-extensions"></a>VM uzantıları yeniden çalıştırın

Bir sanal makine uzantısı toobe gereken durumlar olabilir yeniden çalıştırın. Merhaba uzantısı kaldırarak ve tercih ettiğiniz yürütme yöntemiyle hello uzantısı yeniden çalıştırma bunu yapabilirsiniz. bir uzantı tooremove komutu hello Azure PowerShell modülü ile aşağıdaki hello çalıştırın. Örnek parametre adları kendi değerlerinizle değiştirin.

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Uzantı hello Azure portal kullanarak da kaldırılabilir. toodo için:

1. Bir sanal makineyi seçin.
2. Seçin **uzantıları**.
3. İstenen hello uzantı seçin.
4. Seçin **kaldırma**.

## <a name="common-vm-extensions-reference"></a>Ortak VM uzantıları başvurusu
| Uzantı adı | Açıklama | Daha fazla bilgi |
| --- | --- | --- |
| Windows için özel betik uzantısı |Bir Azure sanal makinesi karşı komut dosyalarını çalıştır |[Windows için özel betik uzantısı](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Windows için DSC uzantısı |PowerShell DSC (İstenen durum Yapılandırması ') uzantısı |[Windows için DSC uzantısı](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure Tanılama Uzantısı |Azure tanılama yönetme |[Azure Tanılama Uzantısı](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Azure VM erişim uzantısı |Kullanıcılar ve kimlik bilgilerini yönetme |[Linux VM erişim uzantısı](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
