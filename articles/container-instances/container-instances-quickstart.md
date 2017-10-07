---
title: "aaaCreate ilk Azure kapsayıcı örnekleri kapsayıcı | Azure belgeleri"
description: "Azure Container Instances’ı dağıtma ve kullanmaya başlama"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a>Azure Container Instances’da ilk kapsayıcınızı oluşturma

Azure kapsayıcı örnekleri kolay toocreate kolaylaştırır ve Azure kapsayıcı yönetin. Bu Hızlı Başlangıç, Azure içinde bir kapsayıcı oluşturacak ve toohello kullanıma Internet ortak IP adresine sahip. Bu işlem tek bir komutla tamamlanır. Yalnızca birkaç saniye içinde tarayıcınızda şunu görürsünüz:

![Azure Container Instances kullanılarak dağıtılmış uygulama tarayıcıda görüntüleniyor][aci-app-browser]

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.12 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Azure Container Instances örnekleri Azure kaynaklarıdır ve Azure kaynaklarının dağıtıldığı ve yönetildiği mantıksal bir koleksiyon olan Azure kaynak gruplarına yerleştirilmelidir.

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a>Bir kapsayıcı oluşturma

Bir ad, Docker görüntüsü ve bir Azure kaynak grubu sağlayarak kapsayıcı oluşturabilirsiniz. İsteğe bağlı olarak hello kapsayıcı toohello getirebilir Internet ortak IP adresine sahip. Bu durumda, [Node.js](http://nodejs.org) ile yazılan, çok basit bir web uygulamasını barındıran bir kapsayıcı kullanacağız.

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

Birkaç saniye içinde bir yanıt tooyour isteği almanız gerekir. Merhaba kapsayıcı başlangıçta olacak bir **oluşturma** durumu, ancak bu işlem birkaç saniye içinde başlamalıdır. Hello kullanarak hello durumunu kontrol edebilirsiniz `show` komutu:

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

Merhaba Çıktı Hello altındaki hello kapsayıcının sağlama durumunu ve IP adresini görürsünüz:

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

Merhaba kapsayıcı toohello taşır sonra **başarılı** durumunda, ulaşana, sağlanan başlangıç IP adresi kullanarak hello tarayıcıda. 

![Azure Container Instances kullanılarak dağıtılmış uygulama tarayıcıda görüntüleniyor][aci-app-browser]

## <a name="pull-hello-container-logs"></a>Merhaba kapsayıcı günlüklerini

Merhaba günlükleri hello kullanılarak oluşturulan hello kapsayıcısı için çekme `logs` komutu:

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

Çıktı:

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a>Merhaba kapsayıcısını silmek

Merhaba kapsayıcıyla bittiğinde hello kullanarak kaldırabilirsiniz `delete` komutu:

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç bölümünde kullanılan hello kapsayıcısı için tüm hello kod [github'da][app-github-repo], kendi Dockerfile yanı sıra. Kendiniz oluşturma ve tooAzure kapsayıcı hello Azure kapsayıcı kayıt defterini kullanarak örnekleri dağıtma tootry isterseniz, toohello Azure kapsayıcı örnekleri öğretici devam edin.

> [!div class="nextstepaction"]
> [Azure Container Instances öğreticileri](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png