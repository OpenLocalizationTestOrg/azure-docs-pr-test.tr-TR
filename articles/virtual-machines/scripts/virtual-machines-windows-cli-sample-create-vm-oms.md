---
title: "Azure CLI betik örnek - OMS izleme ile bir Windows Server 2016 VM oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - OMS izleme ile bir Windows Server 2016 VM oluşturma"
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
ms.author: rclaus
ms.openlocfilehash: ddb191163061dc47712e024c8c1d7a6f4bdf325b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a>Bir VM Operations Management Suite ile izleme

Bu komut dosyasını bir Azure sanal makinesi oluşturur, Operations Management Suite (OMS) Aracısı'nı yükler ve bir OMS çalışma sistemiyle kaydeder. Betik çalıştıktan sonra sanal makine OMS konsolunda görünür.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "hızlı VM oluştur")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut, bir kaynak grubu, sanal makine ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) | Sanal makine oluşturur ve ağ kartı, sanal ağ, alt ağ ve NSG bağlanır. Bu komut ayrıca kullanılacak sanal makine görüntüsü ve yönetici kimlik bilgilerini belirtir.  |
| [Azure vm uzantısı kümesi](https://docs.microsoft.com/cli/azure/vm/extension#set) | VM uzantısı bir sanal makineye karşı çalışır. Bu durumda, Operations Management Suite Aracı Uzantısı OMS Aracısı'nı yüklemek ve bir OMS çalışma alanında VM kaydetmek için kullanılır. |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek sanal makine CLI kod örnekleri bulunabilir [Azure Windows VM belgelerine](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
