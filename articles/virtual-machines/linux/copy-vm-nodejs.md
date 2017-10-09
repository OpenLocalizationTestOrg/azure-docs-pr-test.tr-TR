---
title: "aaaCreate hello Azure CLI 1.0 ile Linux VM kopyasını | Microsoft Docs"
description: "Nasıl bir Azure Linux sanal makineniz ile kopyasını toocreate hello Azure CLI 1.0 hello Resource Manager dağıtım modelinde öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a>Azure CLI 1.0 hello ile Azure üzerinde çalışan Linux sanal makine bir kopyasını oluşturun
Bu makalede nasıl toocreate Azure sanal makine (VM) çalışan Linux kullanarak bir kopyasını hello Resource Manager dağıtım modeli gösterilmektedir. İlk olarak, hello işletim sistemi ve veri diskleri tooa yeni kapsayıcı, kopyalayın sonra hello ağ kaynakları ayarlamak ve hello yeni sanal makine oluşturun.

Ayrıca [karşıya yükleme ve özel disk görüntüsünden bir VM oluşturma](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- Azure CLI 1.0 – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için

## <a name="before-you-begin"></a>Başlamadan önce
Merhaba hello adımları başlamadan önce aşağıdaki önkoşulları karşıladığından emin olun:

* Merhaba sahip [Azure CLI](../../cli-install-nodejs.md) makinenizde yüklenip. 
* Ayrıca, mevcut bir Azure Linux VM'i hakkında bazı bilgiler gerekir:

| Kaynak VM bilgileri | Burada tooget, |
| --- | --- |
| VM adı |`azure vm list` |
| Kaynak grubu adı |`azure vm list` |
| Konum |`azure vm list` |
| Depolama hesabı adı |`azure storage account list -g <resourceGroup>` |
| Kapsayıcı adı |`azure storage container list -a <sourcestorageaccountname>` |
| Kaynak VM VHD dosya adı |`azure storage blob list --container <containerName>` |

* Yeni VM'nin hakkında bazı seçenekleri toomake gerekir:   <br> -Kapsayıcı adı   <br> -VM adı   <br> -VM boyutu   <br> -vNet adı   <br> -Alt ağ adı   <br> -IP adı   <br> -NIC adı

## <a name="login-and-set-your-subscription"></a>Oturum açma ve aboneliğinizi ayarlayın
1. Oturum açma toohello CLI.

    ```azurecli
    azure login
    ```
2. Kaynak Yöneticisi modunda olduğundan emin olun.

    ```azurecli
    azure config mode arm
    ```
3. Merhaba doğru aboneliğin ayarlayın. 'Azure hesabı listesi' toosee kullanabileceğiniz tüm aboneliklerinizi.

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a>Merhaba VM Durdur
Durdurun ve hello kaynak VM serbest bırakma. Aboneliğiniz ve kaynak grubu adları 'azure vm listesi' tooget hello VM'ler tümünün listesini kullanabilirsiniz.

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a>Merhaba VHD kopyalayın
Merhaba kaynak depolama toohello hedef hello kullanarak hello VHD kopyalayabilirsiniz `azure storage blob copy start`. Bu örnekte, biz toocopy hello VHD toohello kalacaklarını aynı depolama hesabı, ancak farklı bir kapsayıcı.

toocopy hello VHD tooanother hello kapsayıcısında aynı depolama hesabı, türü:

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a>Yeni VM için Hello sanal ağ kur ayarlama
Yeni VM için bir sanal ağ ve NIC ayarlayın. 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a>Oluşturma yeni VM hello
Karşıya yüklenen sanal diskten bir VM artık oluşturabilirsiniz [resource manager şablonu kullanarak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) veya hello hello URI tooyour belirterek CLI disk yazarak kopyalanan:

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a>Sonraki adımlar
toolearn nasıl toouse Azure CLI toomanage, yeni bir sanal makine bkz [hello Azure Resource Manager için Azure CLI komutları](../azure-cli-arm-commands.md).

