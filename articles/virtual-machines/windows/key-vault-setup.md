---
title: "Anahtar kasası için Windows Vm'leri Azure Kaynak Yöneticisi'nde yedekleme aaaSet | Microsoft Docs"
description: "Nasıl bir Azure Resource Manager sanal makinesi ile kullanmak için anahtar kasası yukarı tooset."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a>Sanal makineler Azure Kaynak Yöneticisi'nde için anahtar kasasını oluşturup

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

Gizli/sertifikalar, anahtar kasasının hello kaynak sağlayıcısı tarafından sağlanan kaynaklar olarak Azure Kaynak Yöneticisi yığınında modellenir. Anahtar kasası hakkında daha fazla toolearn bakın [Azure anahtar kasası nedir?](../../key-vault/key-vault-whatis.md)

> [!NOTE]
> 1. Azure Resource Manager sanal makinelerle kullanılan anahtar kasası toobe için sırayla hello **EnabledForDeployment** tootrue anahtar kasası özelliği ayarlanmalıdır. Çeşitli istemciler bunu yapabilirsiniz.
> 2. Merhaba anahtar kasası gereksinimlerini toobe oluşturulan aynı abonelikte ve konumda sanal makine hello gibi hello.
>
>

## <a name="use-powershell-tooset-up-key-vault"></a>Anahtar kasası yukarı PowerShell tooset kullanın
toocreate PowerShell kullanarak bir anahtar kasası bkz [Azure anahtar kasası ile çalışmaya başlama](../../key-vault/key-vault-get-started.md#vault).

Yeni anahtar kasalarını için bu PowerShell cmdlet'ini kullanabilirsiniz:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

Varolan anahtar kasalarını için bu PowerShell cmdlet'ini kullanabilirsiniz:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a>Bize CLI tooset anahtar kasası ayarlama
toocreate hello komut satırı arabirimi (CLI) kullanarak bir anahtar kasası bkz [anahtar kasası CLI kullanarak yönetme](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

CLI için hello dağıtım ilkesi atamadan önce toocreate hello anahtar kasası sahip. Bu komutu aşağıdaki hello kullanarak yapabilirsiniz:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Anahtar kasası yukarı şablonları tooset kullanın
Bir şablon kullanırken tooset hello gereksinim `enabledForDeployment` özelliği çok`true` hello anahtar kasası kaynak için.

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
