---
title: "hello Azure kapsayıcı kayıt defteri gelen aaaDeploy tooAzure kapsayıcı örnekleri | Azure belgeleri"
description: "Hello Azure kapsayıcı kayıt defteri tooAzure kapsayıcı örneklerinden dağıtma"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a>Hello Azure kapsayıcı kayıt defteri tooAzure kapsayıcı örneklerinden dağıtma

Hello Azure kapsayıcı kayıt defteri Docker kapsayıcısı görüntüleri için bir Azure tabanlı, özel kayıt defteri ' dir. Bu makalede nasıl toodeploy kapsayıcı görüntüleri hello Azure kapsayıcı kayıt defteri tooAzure kapsayıcı örnekleri depolanan yer almaktadır.

## <a name="using-hello-azure-cli"></a>Hello Azure CLI kullanma

Hello Azure CLI oluşturmak ve Azure kapsayıcı örnekleri kapsayıcılarında yönetmek için komutlar içerir. Özel bir görüntü hello belirtirseniz, `create` komut ayrıca belirtebilirsiniz hello görüntü kayıt defteri parola gerekli tooauthenticate hello kapsayıcı kayıt defteri ile.

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

Merhaba `create` de destekler hello belirterek komutu `registry-login-server` ve `registry-username`. Ancak, hello oturum açma hello Azure kapsayıcı kayıt defteri için her zaman sunucusudur *registryname*. azurecr.io ve hello varsayılan kullanıcı adı *registryname*, bu değerler, hello resim adından algılanır açıkça sağlanmadı.

## <a name="using-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu kullanarak

Merhaba ekleyerek bir Azure Resource Manager şablonu Azure kapsayıcı kaydınız hello özelliklerini belirtebilirsiniz `imageRegistryCredentials` hello kapsayıcısı Grup tanımında özelliği:

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

kapsayıcı kayıt defteri parolanızı doğrudan hello şablonunda depolama tooavoid bunu bir gizli olarak saklamanızı öneririz [Azure anahtar kasası](../key-vault/key-vault-manage-with-cli2.md) ve hello kullanılarak hello şablonunda başvuru [arasında yerel tümleştirme Azure Resource Manager ve anahtar kasası hello](../azure-resource-manager/resource-manager-keyvault-parameter.md).

## <a name="using-hello-azure-portal"></a>Hello Azure portalını kullanma

Hello Azure kapsayıcı kayıt defteri kapsayıcı görüntülerinde bulunduruyorsanız, Azure kapsayıcı örnekleri hello Azure portal kullanarak bir kapsayıcı kolayca oluşturabilirsiniz.

1. Hello Azure portal, tooyour kapsayıcı kayıt defteri gidin.

2. Depoları seçin.

    ![Hello Azure kapsayıcı kayıt defteri menüsünde hello Azure portalı][acr-menu]

3. Gelen toodeploy istediğiniz hello depo seçin.

4. Merhaba etiketi sağ hello kapsayıcı görüntü için toodeploy istiyor.

    ![Kapsayıcı Azure kapsayıcı örnekleri ile başlatmak için bağlam menüsü][acr-runinstance-contextmenu]

5. Merhaba kapsayıcı için bir ad ve hello kaynak grubu için bir ad girin. İsterseniz, ayrıca hello varsayılan değerleri değiştirebilirsiniz.

    ![Azure kapsayıcı örnekleri için menü oluşturma][acr-create-deeplink]

6. Merhaba dağıtım işlemi tamamlandıktan sonra IP adresini ve diğer özellikleri toohello kapsayıcı hello bildirimleri bölmesinde toofind grubundan gidebilirsiniz.

    ![Azure kapsayıcı örnekleri kapsayıcı grubu için ayrıntıları görüntüle][aci-detailsview]

## <a name="next-steps"></a>Sonraki adımlar

Nasıl toobuild kapsayıcıları, bunları tooa özel kapsayıcı kayıt defteri gönderme ve tooAzure kapsayıcı örnekleri tarafından dağıtmadan öğrenin [hello öğreticiyi tamamlamak](container-instances-tutorial-prepare-app.md).

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
