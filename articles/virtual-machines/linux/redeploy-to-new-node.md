---
title: Linux sanal makineleri azure'da aaaRedeploy | Microsoft Docs
description: "Nasıl tooredeploy Linux sanal makinelerinin Azure toomitigate SSH bağlantısını keser."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a>Linux sanal makine toonew Azure düğümü yeniden dağıtın
SSH sorunlarını giderme zorluklarla yüz veya uygulamaya erişim tooa Linux sanal makine (VM) Azure'da hello VM dağıtarak yardımcı olabilir. Bir VM yeniden dağıtırken hello VM tooa yeni düğümde hello Azure altyapı taşır ve yeniden çalıştırır. Tüm yapılandırma seçenekleri ve ilişkili kaynakları korunur. Bu makale size nasıl gösterir VM Azure CLI veya hello Azure portal kullanarak bir tooredeploy.

> [!NOTE]
> Bir VM dağıtmanız sonra hello geçici disk kaybolur ve sanal ağ arabirimiyle ilişkilendirilmiş dinamik IP adreslerini güncelleştirilir. 

Seçenekler aşağıdaki hello birini kullanarak bir VM'i yeniden dağıtabilirsiniz. Yalnızca VM toochoose bir seçenek tooredeploy gerekir:

- [Azure CLI 2.0](#azure-cli-20)
- [Azure CLI 1.0](#azure-cli-10)
- [Azure portal](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a>Hello Azure CLI 2.0 kullanın
Son yükleme hello [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).

VM ile dağıtmanız [az vm dağıtın](/cli/azure/vm#redeploy). Aşağıdaki örnek yeniden dağıtır hello hello adlı VM *myVM* adlı hello kaynak grubunda *myResourceGroup*:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a>Hello Azure CLI 1.0 kullanın
Merhaba yüklemek [en son Azure CLI 1.0](../../cli-install-nodejs.md)tooan Azure hesabı oturum ve Kaynak Yöneticisi modunda olduğundan emin olun (`azure config mode arm`).

Aşağıdaki örnek yeniden dağıtır hello hello adlı VM *myVM* adlı hello kaynak grubunda *myResourceGroup*:

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Sonraki adımlar
Tooyour VM bağlantı sorunları yaşıyorsanız, özel Yardım bulabilirsiniz [SSH bağlantı sorunlarını giderme](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [sorun giderme adımları SSH ayrıntılı](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). VM üzerinde çalışan bir uygulama, erişemiyor, ayrıca okuyabilirsiniz [uygulama sorunlarını giderme](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

