---
title: Azure CLI 2.0 kullanarak bir Linux VM aaaCopy | Microsoft Docs
description: "Bilgi nasıl toocreate Azure CLI 2.0 ve yönetilen diskleri kullanarak Azure Linux VM bir kopyası."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a>Azure CLI 2.0 ve yönetilen diskleri kullanarak bir Linux VM bir kopyasını oluşturun


Bu makalede toocreate bir kopyasını kullanarak Linux çalıştıran, Azure sanal makine (VM) nasıl hello Azure CLI 2.0 ve hello Azure Resource Manager dağıtım modeli gösterilmektedir. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Ayrıca [karşıya yükleyin ve bir VHD'den bir VM oluşturma](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Ön koşullar


-   Yükleme [Azure CLI 2.0](/cli/azure/install-az-cli2)

-   İçinde tooan Azure hesabı ile oturum [az oturum açma](/cli/azure/#login).

-   Kopyanızı hello kaynağı olarak bir Azure VM toouse sahip.

## <a name="step-1-stop-hello-source-vm"></a>1. adım: hello kaynak VM Durdur


Kullanarak Hello kaynak VM serbest bırakma [az vm serbest bırakma](/cli/azure/vm#deallocate).
Merhaba aşağıdaki örnek kaldırır hello adlı VM **myVM** hello kaynak grubunda **myResourceGroup**:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a>2. adım: hello kaynak VM kopyalama


bir VM toocopy, hello alttaki sanal sabit diskin bir kopyasını oluşturun. Bu işlem, özel bir VHD yönetilen hello içeren bir Disk oluşturur. kaynak VM aynı yapılandırma ve hello olarak ayarlar.

Azure Yönetilen Diskler hakkında daha fazla bilgi için bkz. [Azure Yönetilen Disklere genel bakış](../windows/managed-disks-overview.md). 

1.  Her VM hello adı ve kendi işletim sistemi diski ile listesinde [az vm listesi](/cli/azure/vm#list). Merhaba aşağıdaki örnek listeler adlı kaynak grubundaki tüm sanal makineleri **myResourceGroup**:
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    Merhaba, benzer toohello aşağıdaki örneğine çıktı:

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  Yeni bir oluşturarak hello disk Kopyala yönetilen diski kullanarak [az disketi](/cli/azure/disk#create). Merhaba aşağıdaki örnekte oluşturur adlı bir disk **myCopiedDisk** adlı disk hello yönetilen **myDisk**:

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  Artık kaynak grubunuzdaki yönetilen hello diskleri kullanarak doğrulayın [az disk listesi](/cli/azure/disk#list). Merhaba aşağıdaki örnek listeler adlı hello kaynak grubundaki yönetilen hello diskler **myResourceGroup**:

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  Çok atla["3. adım: sanal ağ kurma"](#step-3-set-up-a-virtual-network).


## <a name="step-3-set-up-a-virtual-network"></a>3. adım: Sanal ağ ayarlama


Merhaba aşağıdaki isteğe bağlı adımlar yeni bir sanal ağ, alt ağ, genel IP adresi ve sanal ağ arabirim kartı (NIC) oluşturur.

Bir VM amacıyla ya da başka dağıtımlar sorun giderme için kopyalıyorsanız toouse, varolan bir sanal ağda bir VM istemeyebilirsiniz.

Kopyalanan Vm'leriniz için toocreate bir sanal ağ altyapısı istiyorsanız izleyin hello sonraki birkaç adımda. Bir sanal ağ toocreate istemiyorsanız, çok atla[4. adım: bir VM oluşturma](#step-4-create-a-vm).

1.  Kullanarak Hello sanal ağ oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create). Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur **myVnet** ve adlı bir alt ağ **mySubnet**:

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  Kullanarak bir genel IP oluşturun [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create). Merhaba aşağıdaki örnekte oluşturur adlı ortak IP **myPublicIP** hello DNS adı ile **mypublicdns**. (Merhaba DNS adı gerekir benzersiz olması, dolayısıyla benzersiz bir ad sağlayın.)

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  NIC Hello kullanarak oluşturduğunuz [az ağ NIC oluşturma](/cli/azure/network/nic#create).
    Merhaba aşağıdaki örnekte oluşturur adlı bir NIC **myNic** o ekli toothe **mySubnet** alt ağ:

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a>4. adım: bir VM oluşturma

Kullanarak bir VM şimdi oluşturabilirsiniz [az vm oluşturma](/cli/azure/vm#create).

Merhaba kopyalanan hello işletim sistemi diski olarak yönetilen disk toouse belirtin (--attach-os-disk) aşağıdaki gibi:

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a>Sonraki adımlar

toolearn nasıl toouse Azure CLI toomanage, yeni VM bkz [hello Azure Resource Manager için Azure CLI komutları](../azure-cli-arm-commands.md).
