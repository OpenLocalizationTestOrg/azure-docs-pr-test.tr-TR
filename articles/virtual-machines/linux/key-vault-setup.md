---
title: "Azure anahtar kasası Linux VM'ler için yukarı aaaSet | Microsoft Docs"
description: "Nasıl anahtar kasası yukarı tooset ile bir Azure Resource Manager sanal makine ile kullanmak için CLI 2.0 hello."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a>Anahtar kasası yukarı tooset ile sanal makineler için Azure CLI 2.0 nasıl hello

Gizli/sertifikalar, anahtar kasası tarafından sağlanan kaynaklar olarak Hello Azure Kaynak Yöneticisi yığınında modellenir. Azure anahtar kasası hakkında daha fazla toolearn bakın [Azure anahtar kasası nedir?](../../key-vault/key-vault-whatis.md) Azure Kaynak Yöneticisi Vm'leri ile kullanılan anahtar kasası toobe için sırayla hello *EnabledForDeployment* tootrue anahtar kasası özelliği ayarlanmalıdır. Bu makale size gösterir nasıl Azure kullanarak sanal makineleri (VM'ler) ile kullanmak için anahtar kasası yukarı tooset hello Azure CLI 2.0. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Aşağıdaki adımları tooperform ihtiyacınız hello son [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

## <a name="create-a-key-vault"></a>Anahtar kasası oluşturma
Bir anahtar kasası oluşturun ve hello dağıtım ilkesiyle atayın [az keyvault oluşturma](/cli/azure/keyvault#create). Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar kasası `myKeyVault` hello içinde `myResourceGroup` kaynak grubu:

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a>Sanal makineler ile kullanmak için bir anahtar kasası güncelleştirme
Merhaba dağıtım ilkesi olan bir anahtar kasası ile ayarlandığında [az keyvault güncelleştirme](/cli/azure/keyvault#update). Merhaba aşağıdaki güncelleştirmeleri hello adlı anahtar kasası `myKeyVault` hello içinde `myResourceGroup` kaynak grubu:

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a>Anahtar kasası yukarı şablonları tooset kullanın
Bir şablonu kullandığınızda tooset hello gereksinim `enabledForDeployment` özelliği çok`true` şekilde hello anahtar kasası kaynak için:

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a>Sonraki adımlar
Şablonları kullanarak bir anahtar kasası oluşturduğunuzda, sizin yapılandırabileceğiniz diğer seçenekleri için bkz: [bir anahtar kasası oluşturma](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
