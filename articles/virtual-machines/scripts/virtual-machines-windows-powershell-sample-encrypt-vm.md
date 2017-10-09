---
title: "PowerShell komut dosyası örneği - aaaAzure şifrelemek Windows VM | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - Windows VM şifrele"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 80c52a0b734a52a051ed30026b294840fd521143
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a>Azure PowerShell ile Windows sanal makine şifrele

Bu komut dosyasını güvenli bir Azure anahtar kasası, şifreleme anahtarları, Azure Active Directory Hizmet sorumlusu ve bir Windows sanal makine (VM) oluşturur. Merhaba VM hello şifreleme anahtarı anahtar kasası ve hizmet asıl kimlik bilgileri kullanılarak şifrelenir.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate hello dağıtım aşağıdaki hello kullanır. Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [Yeni-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | Azure anahtar kasası bir toostore güvenli veri şifreleme anahtarları gibi oluşturur. |
| [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | Bir şifreleme anahtarı anahtar kasası oluşturur. |
| [AzureRmADServicePrincipal yeni](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | Bir Azure Active Directory hizmet asıl toosecurely kimlik doğrulaması ve Denetim erişim tooencryption tuşları oluşturur. |
| [Set AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | İzinleri hello anahtar kasası toogrant üzerinde hello hizmet asıl erişim tooencryption anahtarları ayarlar. |
| [AzureRmVirtualNetworkSubnetConfig yeni](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Bir alt ağ yapılandırması oluşturur. Bu yapılandırma ile Merhaba sanal ağ oluşturma işleminde kullanılır. |
| [Yeni-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Sanal ağ oluşturur. |
| [AzureRmPublicIpAddress yeni](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Bir ortak IP adresi oluşturur. |
| [AzureRmNetworkSecurityRuleConfig yeni](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Bir ağ güvenlik grubu kural yapılandırması oluşturur. Merhaba NSG oluşturulduğunda bu kullanılan toocreate bir NSG kuralı yapılandırmadır. |
| [AzureRmNetworkSecurityGroup yeni](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Bir ağ güvenlik grubu oluşturur. |
| [Get-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | Alt ağ bilgilerini alır. Bu bilgiler, bir ağ arabirimi oluşturulurken kullanılır. |
| [AzureRmNetworkInterface yeni](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Bir ağ arabirimi oluşturur. |
| [AzureRmVMConfig yeni](/powershell/module/azurerm.compute/new-azurermvmconfig) | Bir VM yapılandırması oluşturur. Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir. Merhaba yapılandırma VM oluşturma sırasında kullanılır. |
| [Yeni-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Bir sanal makine oluşturun. |
| [Get-AzureRmKeyVault](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | Merhaba anahtar kasası hakkında bilgi alır gereken |
| [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | Merhaba hizmet asıl kimlik bilgilerini ve şifreleme anahtarı kullanarak bir VM üzerinde şifrelemeyi etkinleştirir. |
| [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | Merhaba VM şifreleme işlemi Hello durumunu gösterir. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
