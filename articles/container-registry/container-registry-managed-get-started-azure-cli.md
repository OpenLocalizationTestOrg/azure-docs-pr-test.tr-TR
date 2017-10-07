---
title: "aaaCreate özel Docker kapsayıcısı kayıt defteri - Azure CLI | Microsoft Docs"
description: "Oluşturma ve yönetme özel Docker kapsayıcısı kayıt defterleri hello Azure CLI 2.0 ile çalışmaya başlama"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a>Hello Azure CLI kullanarak bir yönetilen kapsayıcı kayıt defteri oluşturma

Azure Container Registry, özel Docker kapsayıcı görüntülerini depolamak için kullanılan bir yönetilen Docker kapsayıcı kayıt defteridir. Bu kılavuzu ayrıntıları Hello Azure CLI kullanarak yönetilen Azure kapsayıcı kayıt defteri örneği oluşturma.

Yönetilen Azure kapsayıcı kayıt defterleri önizleme aşamasındadır ve tüm bölgelerde kullanılamaz.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westcentralus* konumu.

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a>Kapsayıcı kayıt defteri oluşturma

Hello kullanarak bir ACR örneği oluşturma [az acr oluşturmak](/cli/azure/acr#create) komutu.

> [!NOTE]
> Bir kayıt defteri oluştururken yalnızca harf ve sayı içeren genel olarak benzersiz bir üst düzey etki alanı adı sağlayın.

 Merhaba kayıt defteri adı hello örnekte *myContainerRegistry1*, kendi benzersiz adı değiştirin.

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

Merhaba kayıt oluşturulduğunda hello çıkış benzer toohello aşağıda verilmiştir:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a>TooACR örneğinde oturum

İletme ve kapsayıcı görüntüleri çekme önce toohello ACR örneğinde oturum açmanız gerekir. toodo, kullanın hello [az acr oturum açma](/cli/azure/acr#login) komutu.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

Merhaba komut tamamlandıktan sonra 'Başarılı oturum açma' iletisi döndürür.

## <a name="use-azure-container-registry"></a>Azure Container Registry’yi kullanma

### <a name="list-container-images"></a>Kapsayıcı görüntülerini listeleme

Kullanım hello `az acr` CLI komutları tooquery hello görüntüleri ve bir havuzda etiketler.

> [!NOTE]
> Şu anda, kapsayıcı kayıt defteri hello desteklemiyor `docker search` komutu tooquery görüntüler ve etiketler için.

### <a name="list-repositories"></a>Depoları listeleme

Merhaba aşağıdaki örnek JSON (JavaScript nesne gösterimi) biçiminde bir kayıt defterindeki hello depoları listeler:

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>Etiketleri listeleme

Merhaba aşağıdaki örnek listeler hello hello etiketlerini **samples/nginx** JSON biçiminde deposu:

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç bölümünde hello Azure CLI kullanarak yönetilen Azure kapsayıcı kayıt defteri örneği oluşturduğunuzu düşünün.

> [!div class="nextstepaction"]
> [Merhaba Docker CLI kullanarak ilk görüntünüzü bildirme](container-registry-get-started-docker-cli.md)
