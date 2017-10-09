---
title: "Anahtar kasası Linux VM'ler için yukarı aaaSet hello Azure CLI 1.0 ile | Microsoft Docs"
description: "Nasıl anahtar kasası yukarı tooset ile bir Azure Resource Manager sanal makine ile kullanmak için Azure CLI 1.0 hello."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a>Sanal makine Azure Kaynak Yöneticisi'nde hello Azure CLI 1.0 için anahtar kasasını oluşturup
Gizli/sertifikalar, anahtar kasasının hello kaynak sağlayıcısı tarafından sağlanan kaynaklar olarak Hello Azure Kaynak Yöneticisi yığınında modellenir. Azure anahtar kasası hakkında daha fazla toolearn bakın [Azure anahtar kasası nedir?](../../key-vault/key-vault-whatis.md) Azure Resource Manager sanal makinelerle kullanılan anahtar kasası toobe için sırayla hello *EnabledForDeployment* tootrue anahtar kasası özelliği ayarlanmalıdır. Çeşitli istemciler bunu yapabilirsiniz. Bu makale size nasıl gösterir anahtar kasası yukarı tooset Azure sanal makineler ile kullanmak için.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlayın

- [Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için

## <a name="use-cli-10-tooset-up-key-vault"></a>Anahtar kasası yukarı CLI 1.0 tooset kullanın
toocreate hello komut satırı arabirimi (CLI) kullanarak bir anahtar kasası bkz [anahtar kasası CLI kullanarak yönetme](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

CLI 1.0 için hello dağıtım ilkesi atamadan önce toocreate hello anahtar kasası sahip. Ardından, komutu aşağıdaki hello kullanarak hello İlkesi atayabilirsiniz:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Anahtar kasası yukarı şablonları tooset kullanın
Bir şablonu kullandığınızda tooset hello gereksinim `enabledForDeployment` özelliği çok`true` hello anahtar kasası kaynak için.

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

Şablonları kullanarak bir anahtar kasası oluşturduğunuzda, sizin yapılandırabileceğiniz diğer seçenekleri için bkz: [bir anahtar kasası oluşturma](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
