---
title: "aaaAzure CLI betik örnek - Windows VM şifrelemek | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - VM Windows şifrele"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 7a9928467f818cd5358d3d19bff5129d8fa21313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a>Azure'da Windows sanal makine şifrele

Bu komut dosyasını güvenli bir Azure anahtar kasası, şifreleme anahtarları, Azure Active Directory Hizmet sorumlusu ve bir Windows sanal makine (VM) oluşturur. Merhaba VM hello şifreleme anahtarı anahtar kasası ve hizmet asıl kimlik bilgileri kullanılarak şifrelenir.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını bir kaynak grubu, Azure anahtar kasası, hizmet asıl, sanal makine, komutları toocreate aşağıdaki hello kullanır ve tüm kaynakları ilgili. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az keyvault oluşturma](https://docs.microsoft.com/cli/azure/keyvault#create) | Azure anahtar kasası bir toostore güvenli veri şifreleme anahtarları gibi oluşturur. |
| [az keyvault anahtarı oluşturma](https://docs.microsoft.com/cli/azure/keyvault/key#create) | Bir şifreleme anahtarı anahtar kasası oluşturur. |
| [az ad sp oluşturma-için-rbac](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | Bir Azure Active Directory hizmet asıl toosecurely kimlik doğrulaması ve Denetim erişim tooencryption tuşları oluşturur. |
| [az keyvault-ilkesini ayarlama](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | İzinleri hello anahtar kasası toogrant üzerinde hello hizmet asıl erişim tooencryption anahtarları ayarlar. |
| [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) | Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır. Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.  |
| [az vm şifrelemeyi etkinleştir](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | Merhaba hizmet asıl kimlik bilgilerini ve şifreleme anahtarı kullanarak bir VM üzerinde şifrelemeyi etkinleştirir. |
| [az vm şifreleme Göster](https://docs.microsoft.com/cli/azure/vm/encryption#show) | Merhaba VM şifreleme işlemi Hello durumunu gösterir. |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).
