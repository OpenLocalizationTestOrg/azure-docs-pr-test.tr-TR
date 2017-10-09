---
title: "CLI komut dosyası örneği - aaaAzure ile NGINX bir Linux VM oluşturma | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - ile NGINX bir Linux VM oluşturma"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a>İle NGINX bir VM oluşturma

Bu komut dosyasını bir Azure sanal makine oluşturur ve hello Azure sanal makine özel betik uzantısının tooinstall NGINX kullanır. Merhaba komut dosyasını çalıştırdıktan sonra hello genel IP adresi hello sanal makinenin demo Web sitesine erişebilir.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a>Özel Betik Uzantısı

Merhaba özel betik uzantısı hello sanal makine bu betiğini kopyalar. Merhaba betik tooinstall ardından çalıştırın ve bir NGINX web sunucusu yapılandırın. 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) | Merhaba sanal makine oluşturur. Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.  |
| [az vm-bağlantı noktası Aç](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Bir ağ güvenlik grubu kural tooallow oluşturur gelen trafiği. Bu örnekte, bağlantı noktası 80 HTTP trafiği için açıldı. |
| [Azure vm uzantısı kümesi](https://docs.microsoft.com/cli/azure/vm/extension#set) | Ekler ve bir sanal makine uzantısı tooa VM çalıştırır. Bu örnekte kullanılan tooinstall NGINX hello özel komut dosyası uzantısıdır.|
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
