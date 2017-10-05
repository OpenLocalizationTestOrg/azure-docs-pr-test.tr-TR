---
title: "Azure CLI örnek komut dosyası - yük dengeli sanal Machin ölçek kümesindeki AMPUL yığını dağıtma | Microsoft Docs"
description: "Bir yük AMPUL yığınında dağıtmak için bir özel betik uzantısı kullanın = dengeli sanal makine ölçek Azure üzerinde ayarlayın."
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
ms.openlocfilehash: 4007e8c85c0ff24bf5030881eac666582714eae3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>Yük dengeli sanal makine ölçek kümesi AMPUL yığınında dağıtma

Bu örnek, bir sanal makine ölçek kümesi oluşturur ve her bir sanal makine ölçek kümesindeki AMPUL yığında dağıtmak için özel bir komut dosyası çalıştıran uzantı uygular.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "sanal makine ölçek AMPUL yığınla kümesi oluşturma")]

## <a name="connect"></a>Bağlan

Vm'leriniz ve, Ölçek nasıl bağlayacağınızı görmek için bu kodu kullanın ayarlayın.

[!code-azurecli[Ana](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "erişim sanal makine ölçek kümesi")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Kaynak grubu, Ölçek kümesini ve sanal makineleri kaldırmak için aşağıdaki komutu çalıştırın ve ilişkili tüm kaynakları.

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut, bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilişkili kaynakları oluşturmak için aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az vmss oluşturma](https://docs.microsoft.com/cli/azure/vmss#create) | Bir sanal makine ölçek kümesi oluşturur |
| [az ağ lb kuralı oluşturma](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Yük dengeli bir uç nokta ekleyin |
| [az vmss uzantı kümesi](https://docs.microsoft.com/cli/azure/vmss/extension#set) | VM Dağıtım üzerinde özel komut dosyasını çalıştırır uzantısı oluşturma |
| [az vmss güncelleştirme-örnekleri](https://docs.microsoft.com/cli/azure/vmss#update-instances) | Özel betik uzantısı ölçek kümesi uygulanmadan dağıtılan VM örnekleri çalıştırın. |
| [az vmss ölçek](https://docs.microsoft.com/cli/azure/vmss#scale) | Daha fazla VM örnekleri ekleyerek kümesini ölçeklendirin. Bunlar dağıtıldığında özel bir komut dosyası bunlar üzerinde çalışır. |
| [az ağ ortak IP listesi](https://docs.microsoft.com/cli/azure/network/public-ip#list) | Örneği tarafından oluşturulan VM'ler IP adreslerini alın. |
| [az ağ lb Göster](https://docs.microsoft.com/cli/azure/network/lb#show) | Ön uç ve arka uç yük dengeleyici tarafından kullanılan bağlantı noktaları alın. |

## <a name="next-steps"></a>Sonraki adımlar

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek sanal makine CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
