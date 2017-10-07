---
title: "aaaAzure hızlı başlangıç - VM CLI oluşturun | Microsoft Docs"
description: "Hızlı bir şekilde hello Azure CLI toocreate sanal makinelerle öğrenin."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a>Hello Azure CLI ile Linux sanal makine oluşturma

Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin. Ubuntu server çalıştıran bir sanal makine Hello Azure CLI toodeploy kullanarak bu kılavuzu ayrıntıları. Merhaba sunucu dağıtıldığında, bir SSH bağlantısı oluşturulur ve bir NGINX Web sunucusu yüklenir.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Sanal makine oluşturma

Bir VM ile Merhaba oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu. 

Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* ve zaten bir varsayılan anahtar konumda yoksa, SSH anahtarları oluşturur. toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

Merhaba VM oluşturduğunuzda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir. Merhaba not edin `publicIpAddress`. Kullanılan tooaccess hello VM adresidir.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Web trafiği için 80 numaralı bağlantı noktasını açın 

Varsayılan olarak, Azure’a dağıtılmış Linux sanal makinelerinde yalnızca SSH bağlantılarına izin verilir. Bu VM toobe bir Web sunucusu olacaksa, hello Internet gelen tooopen bağlantı noktası 80 gerekir. Kullanım hello [az vm Aç-port](/cli/azure/vm#open-port) komutu tooopen hello istenen bağlantı noktası.  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a>VM’ye SSH uygulama

Kullanım hello aşağıdaki toocreate SSH oturumu hello sanal makineyle bir komutu. Emin tooreplace olun  *<publicIpAddress>*  hello ile sanal makinenize genel IP adresini düzeltin.  Yukarıdaki örneğimizde IP adresi *40.68.254.142* şeklindedir.

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a>NGINX yükleme

Kullanım hello aşağıdaki komut dosyası tooupdate paket kaynaklarını bash ve hello son NGINX paketini yükleyin. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a>Merhaba NGINX Karşılama sayfasını görüntüle

Yüklü NGINX ve bağlantı noktası 80, VM'den hello Internet - üzerinde şimdi açık seçim tooview hello varsayılan NGINX Hoş Geldiniz sayfasını bir web tarayıcısı kullanabilirsiniz. Emin toouse hello olması *Publicıpaddress* toovisit hello varsayılan sayfa belgelenmiştir. 

![Varsayılan NGINX sitesi](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a>Kaynakları temizleme

Artık gerektiğinde Merhaba kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta basit bir sanal makine ve bir ağ güvenlik grubu kuralı dağıtıp, bir web sunucusu yüklediniz. Azure sanal makinelerde hakkında daha fazla toolearn toohello öğretici Linux VM'ler için devam edin.


> [!div class="nextstepaction"]
> [Azure Linux sanal makine öğreticileri](./tutorial-manage-vm.md)
