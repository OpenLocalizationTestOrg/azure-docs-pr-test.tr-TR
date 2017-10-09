---
title: "aaaAzure CLI komut dosyası örneği - hızlı Oluştur bir Windows Server 2016 VM | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - hızlı bir Windows Server 2016 VM oluştur"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rickstercdn
ms.openlocfilehash: 4c736ce9e2ecc9ee75b34f903cad52c9c0ee0707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a>Hello Azure CLI ile bir sanal makineyi hızlı oluşturma

Bu komut dosyasını Windows Server 2016 çalıştıran bir Azure sanal makine oluşturur. Merhaba komut dosyasını çalıştırdıktan sonra hello sanal makine bir Uzak Masaüstü bağlantısı üzerinden erişebilirsiniz.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) | Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve ağ güvenlik grubu bağlanır. Bu komut ayrıca kullanılan hello sanal makine görüntü toobe belirtir ve yönetici kimlik bilgileri.  |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
