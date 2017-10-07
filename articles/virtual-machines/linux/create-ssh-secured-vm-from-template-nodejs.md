---
title: "Azure CLI 1.0 ile bir Azure şablonu kullanarak bir Linux VM aaaCreate | Microsoft Docs"
description: "Hello Azure CLI 1.0 ve Azure Resource Manager şablonu kullanarak Azure'da bir Linux VM oluşturma."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a>Azure CLI 1.0 bir Azure Resource Manager şablonu kullanarak Linux VM bir toocreate hello nasıl
Bu makalede nasıl tooquickly hello Azure CLI 1.0 ve Azure Resource Manager şablonu kullanarak bir Linux sanal makine dağıtma gösterilir. Merhaba makale gerektirir:

* bir Azure hesabı ([ücretsiz deneme sürümü edinin](https://azure.microsoft.com/pricing/free-trial/)).
* Merhaba [Azure CLI 1.0](../../cli-install-nodejs.md) oturum açarken `azure login`.
* Hello Azure CLI *olmalıdır* Azure Resource Manager moduna `azure config mode arm`.

Hello kullanarak bir Linux VM şablonu da hızlı bir şekilde dağıtabilirsiniz [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#quick-command-summary) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için

## <a name="quick-command-summary"></a>Hızlı Komut Özeti
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a>Ayrıntılı Kılavuz
Şablonları toocreate sanal makineleri Azure üzerinde toocustomize istediğiniz hello başlatma, kullanıcı adları ve ana bilgisayar adları gibi ayarları sırasında ayarlarla sağlar. Bu makalede; SSH'ye açık, 22 numaralı bağlantı noktasına sahip bir ağ güvenlik grubu (NSG) ile birlikte Ubuntu VM'yi kullanarak bir Azure şablonu başlatıyoruz.

Azure Resource Manager şablonları, bir defalık basit görevler (örneğin, bu makalede yapıldığı gibi bir Ubuntu VM'nin başlatılması) için kullanılabilen JSON dosyalarıdır.  Azure şablonları kullanılan tooconstruct Azure yapılandırmalarını tüm ortamları gibi bir test, geliştirme veya Üretim dağıtımı yığını de olabilir.

## <a name="create-hello-linux-vm"></a>Merhaba Linux VM oluşturma
Kod örnekteki nasıl aşağıdaki hello toocall `azure group create` toocreate bir kaynak grubu ve hello sırasında bir SSH güvenlikli Linux VM dağıtmak kullanarak aynı zaman [bu Azure Resource Manager şablonu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json). Benzersiz tooyour ortamı toouse adları olması gerekir, örneğin unutmayın. Bu örnekte *myResourceGroup* hello kaynak grubu adı olarak ve *myVM* hello VM adı olarak.

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

Merhaba çıktı hello çıkış bloğuna aşağıdaki gibi görünmelidir:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Bu örnek hello kullanarak bir VM'i dağıtılan `--template-uri` parametresi.  Ayrıca indirin veya yerel olarak bir şablon oluşturmak ve hello kullanarak hello şablonunu geçirmek `--template-file` bağımsız değişken olarak bir yol toohello şablon dosyası parametresiyle. Hello Azure CLI hello şablon tarafından gereken hello parametrelerini ister.

## <a name="next-steps"></a>Sonraki adımlar
Arama hello [Şablon Galerisi](https://azure.microsoft.com/documentation/templates/) toodiscover hangi uygulama çerçeveleri toodeploy sonraki.

