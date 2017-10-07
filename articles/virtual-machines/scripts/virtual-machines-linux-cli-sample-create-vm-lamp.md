---
title: "aaaAzure CLI komut dosyası örneği - hello AMPUL yığını yük dengelemeli mimarilerde sanal Machin ölçek kümesindeki dağıtma | Microsoft Docs"
description: "Kullanan bir özel betik uzantısı toodeploy hello AMPUL yığını bir yük dengeli sanal makineyi ölçeği Azure üzerinde Ayarla =."
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
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>Yük dengeli sanal makine ölçek kümesindeki Hello AMPUL yığını dağıtma

Bu örnek, bir sanal makine ölçek kümesi oluşturur ve bir özel komut dosyası toodeploy hello AMPUL yığını hello ölçek kümesindeki her bir sanal makine üzerinde çalışan bir uzantı uygular.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a>Bağlan

Bu kod toosee tooconnect tooyour VM'ler ve, Ölçek nasıl ayarlanacağını kullanın.

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Komut tooremove hello kaynak grubu, hello ölçek kümesini ve sanal makineleri ve tüm ilgili kaynaklar aşağıdaki hello çalıştırın.

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilgili kaynaklar aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az vmss oluşturma](https://docs.microsoft.com/cli/azure/vmss#create) | Bir sanal makine ölçek kümesi oluşturur |
| [az ağ lb kuralı oluşturma](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Yük dengeli bir uç nokta ekleyin |
| [az vmss uzantı kümesi](https://docs.microsoft.com/cli/azure/vmss/extension#set) | VM Dağıtım üzerinde hello özel betik çalıştıran hello uzantısı oluşturma |
| [az vmss güncelleştirme-örnekleri](https://docs.microsoft.com/cli/azure/vmss#update-instances) | Merhaba özel komut dosyası hello uzantısı uygulanmadan önce dağıtılan hello VM örnekleri üzerinde çalıştırma toohello ölçek kümesi. |
| [az vmss ölçek](https://docs.microsoft.com/cli/azure/vmss#scale) | Daha fazla VM örnekleri ekleyerek ayarlayın hello ölçek ölçeklendirin. Bunlar dağıtıldığında hello özel betik bunlar üzerinde çalışır. |
| [az ağ ortak IP listesi](https://docs.microsoft.com/cli/azure/network/public-ip#list) | Merhaba hello örneği tarafından oluşturulan VM'ler Hello IP adreslerini alın. |
| [az ağ lb Göster](https://docs.microsoft.com/cli/azure/network/lb#show) | Merhaba ön uç ve arka uç hello yük dengeleyici tarafından kullanılan bağlantı noktaları alın. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
