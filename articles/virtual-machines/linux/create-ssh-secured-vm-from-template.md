---
title: "bir şablondan bir Linux VM azure'da aaaCreate | Microsoft Docs"
description: "Nasıl toouse hello Azure CLI 2.0 toocreate bir Resource Manager şablondan bir Linux VM"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>Nasıl toocreate Azure Resource Manager şablonları kullanarak Linux sanal makine
Bu makale size nasıl tooquickly dağıtmak Azure Resource Manager şablonları ve hello Azure CLI 2.0 ile Linux sanal makine (VM) gösterir. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).


## <a name="templates-overview"></a>Şablonlara genel bakış
Azure Resource Manager şablonları hello altyapısı ve Azure çözümünüzü yapılandırmasını tanımlayan JSON dosyalarıdır. Bir şablon kullanarak çözümünü yaşam döngüsü boyunca defalarca dağıtabilir ve kaynaklarınızın tutarlı bir durumda dağıtıldığından emin olabilirsiniz. toolearn hello şablon ve onu nasıl oluşturmak hello biçimi hakkında daha fazla bilgi görmek [, ilk Azure Resource Manager şablonu oluşturma](../../azure-resource-manager/resource-manager-create-first-template.md). tooview hello JSON söz dizimi kaynak türleri için bkz: [kaynakları tanımlayan Azure Resource Manager şablonları](/azure/templates/).


## <a name="create-resource-group"></a>Kaynak grubu oluşturma
Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. Bir kaynak grubu bir sanal makine önce oluşturulması gerekir. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupVM* hello içinde *eastus* bölge:

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Sanal makine oluşturma
Merhaba aşağıdaki örnekte oluşturur bir VM'den [bu Azure Resource Manager şablonu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) ile [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create). Merhaba içeriğine gibi kendi SSH ortak anahtarını Hello değerini sağlamalısınız *~/.ssh/id_rsa.pub*. SSH anahtar çifti toocreate gerekirse bkz [nasıl toocreate ve kullanım bir SSH çifti Azure Linux VM'ler için anahtar](mac-create-ssh-keys.md).

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

Bu örnekte, Github'da depolanan bir şablon belirtilen. Ayrıca indirin veya bir şablon oluşturmak ve hello ile Merhaba yerel bir yol belirtin aynı `--template-file` parametresi.

tooSSH tooyour VM elde hello ortak IP adresiyle [az ağ ortak IP Göster](/cli/azure/network/public-ip#show):

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

Bundan sonra normal olarak SSH tooyour VM yapabilirsiniz:

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>Sonraki adımlar
Bu örnekte, temel bir Linux VM oluşturdunuz. Merhaba, uygulama çerçeveleri dahil etmek veya daha karmaşık ortamları oluşturma daha fazla Resource Manager şablonları için Gözat [Azure hızlı başlangıç Şablon Galerisi](https://azure.microsoft.com/documentation/templates/).
