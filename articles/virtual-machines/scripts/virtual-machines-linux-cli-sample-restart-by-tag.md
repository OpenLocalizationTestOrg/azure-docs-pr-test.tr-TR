---
title: "aaaAzure CLI komut dosyası örneği - VMs yeniden | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - yeniden başlatma VM'ler etiketi ve kimliği"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a>Sanal makineleri yeniden başlatın

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

Bu örnek birkaç yolu tooget bazı sanal makineleri gösterir ve bunları yeniden başlatın.

Merhaba hello kaynak grubunda ilk tüm hello VM'ler yeniden başlatır.

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

Merhaba ikinci alır hello etiketli kullanarak VM'ler `az resouce list` VM'ler toohello kaynakları filtreler ve bu sanal makineleri yeniden başlatır.

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

Bu örnek, bir Bash kabuğunda çalışır. Windows istemcisi üzerinde Azure CLI betikleri çalıştırma seçenekleri için bkz [Windows hello Azure CLI çalıştıran](../windows/cli-options.md).


## <a name="sample-script"></a>Örnek komut dosyası

Merhaba örnek üç komut dosyasına sahiptir.
ilk hello sanal makineler hello.
Sağlanan her bir VM toobe beklemeden Hello komutu döndürecek şekilde hello Hayır bekleme seçeneği kullanır.
Merhaba, ikinci tam olarak sağlanan hello VM'ler toobe için bekler.
sağlanan tüm hello VM'ler Hello üçüncü komut dosyası yeniden başlatır ve ardından sanal makineleri yalnızca hello etiketli.

### <a name="provision-hello-vms"></a>Merhaba VM'ler sağlama

Bu komut dosyasını bir kaynak grubu ve üç VM'ler toorestart oluşturur.
İki tanesi etiketlenir.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a>Wait

Bu betik, tüm üç VM'ler sağlanır veya bunlardan birini tooprovision başarısız olana kadar 20 dakikada sağlama durumu hello üzerinde denetler.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a>Merhaba sanal makineleri yeniden başlatın

Bu komut tüm hello VM'ler hello kaynak grubunda yeniden başlatır ve yalnızca etiketli hello VM'ler yeniden başlatır.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grupları, sanal makineleri ve tüm ilişkili kaynakları olabilir.

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilgili kaynaklar aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Merhaba sanal makineler oluşturur.  |
| [az vm listesi](https://docs.microsoft.com/cli/azure/vm#list) | İle kullanılan `--query` tooensure hello VM'ler sağlanan yeniden başlatmadan önce ve sonra tooget hello hello VM'ler toorestart kimliklerini bunları. |
| [az kaynak listesi](https://docs.microsoft.com/cli/azure/vm#list) | İle kullanılan `--query` tooget hello hello etiketini kullanarak hello VM'ler kimliklerini. |
| [az vm yeniden başlatma](https://docs.microsoft.com/cli/azure/vm#list) | Merhaba VM'ler yeniden başlatır. |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
