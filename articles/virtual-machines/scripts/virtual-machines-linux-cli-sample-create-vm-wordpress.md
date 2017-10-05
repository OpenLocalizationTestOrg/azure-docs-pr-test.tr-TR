---
title: "Azure CLI örnek komut dosyası - WordPress ile bir Linux VM oluşturma | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - WordPress ile bir Linux VM oluşturma"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: cc95a190b58cb208ac0b642fc9dc2253e993ca23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-wordpress"></a>WordPress ile bir VM oluşturma

Bu komut dosyasını bir sanal makine oluşturur ve WordPress yüklemek için Azure sanal makine özel betik uzantısı kullanır. Komut dosyasını çalıştırdıktan sonra WordPress yapılandırma sitesinde erişebilirsiniz `http://<public IP of VM>/wordpress`. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "hızlı VM oluştur")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut, bir kaynak grubu, sanal makine ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) | Sanal makine oluşturur ve ağ kartı, sanal ağ, alt ağ ve NSG bağlanır. Bu komut ayrıca kullanılacak sanal makine görüntüsü ve yönetici kimlik bilgilerini belirtir.  |
| [az vm-bağlantı noktası Aç](https://docs.microsoft.com/cli/azure/vm#open-port) | Gelen trafiğe izin vermek için bir ağ güvenlik grubu kural oluşturur. Bu örnekte, bağlantı noktası 80 HTTP trafiği için açıldı. |
| [az vm uzantısı kümesi](https://docs.microsoft.com/cli/azure/vm#create) | Özel betik uzantısının WordPress yüklemek için bir komut dosyası çağırır sanal makine için ekleyin. |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek sanal makine CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
