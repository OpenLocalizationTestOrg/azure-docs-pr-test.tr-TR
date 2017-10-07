---
title: "aaaAzure kapsayıcı örnekleri öğretici - Azure kapsayıcı kayıt defteri hazırlama | Microsoft Docs"
description: "Azure kapsayıcı örnekleri Öğreticisi - Azure kapsayıcı kayıt defteri hazırlama"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Container’lar, Mikro hizmetler, Kumernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Dağıtma ve Azure kapsayıcı kayıt defteri kullanma

Bu iki üç bölümlü öğretici parçasıdır. Merhaba, [önceki adımda](./container-instances-tutorial-prepare-app.md), yazılan basit bir web uygulaması için bir kapsayıcı görüntüsü oluşturuldu [Node.js](http://nodejs.org). Bu öğreticide, bu görüntüyü tooan Azure kapsayıcı kayıt defteri gönderilir. Merhaba kapsayıcı görüntü oluşturmadıysanız çok dönüş[Öğreticisi 1 – Oluştur kapsayıcı görüntü](./container-instances-tutorial-prepare-app.md). 

Hello Azure kapsayıcı kayıt defteri Docker kapsayıcısı görüntüleri için bir Azure tabanlı, özel kayıt defteri ' dir. Bu öğreticide, Azure kapsayıcı kayıt defteri örneğini dağıtma ve kapsayıcı görüntü tooit Ftp'den aracılığıyla açıklanmaktadır. Tamamlanan adımları içerir:

> [!div class="checklist"]
> * Azure kapsayıcı kayıt defteri örneğini dağıtma
> * Azure kapsayıcı kayıt defteri için etiketleme kapsayıcı görüntüsü
> * Görüntü tooAzure kapsayıcı kayıt defteri karşıya yükleme

Sonraki öğreticilerde özel kayıt defteri tooAzure kapsayıcı örnekleri hello kapsayıcı dağıtın.

## <a name="before-you-begin"></a>Başlamadan önce

Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırdığınız gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).

## <a name="deploy-azure-container-registry"></a>Azure kapsayıcı kayıt defteri dağıtın

Azure kapsayıcı kayıt defteri dağıtırken, önce bir kaynak grubu gerekir. Bir Azure kaynak grubu hangi Azure kaynakları dağıtılan yönetilen ve mantıksal bir koleksiyonudur.

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Bu örnekte, bir kaynak grubu adında *myResourceGroup* hello oluşturulan *eastus* bölge.

```azurecli
az group create --name myResourceGroup --location eastus
```

Azure kapsayıcı kayıt defteri ile Merhaba oluşturma [az acr oluşturmak](/cli/azure/acr#create) komutu. bir kapsayıcı kayıt defteri Hello adını **benzersiz olmalıdır**. Aşağıdaki örneğine hello kullanırız hello adı *mycontainerregistry082*.

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

Hello rest Bu öğreticinin kullanırız `<acrname>` seçtiğiniz hello kapsayıcı kayıt defteri adı için bir yer tutucu olarak.

## <a name="container-registry-login"></a>Kapsayıcı kayıt defteri oturum açma

Görüntüleri tooit göndermeden önce tooyour ACR örneğinde oturum açmanız gerekir. Kullanım hello [az acr oturum açma](https://docs.microsoft.com/en-us/cli/azure/acr#login) toocomplete hello işlemi komutu. Oluşturulduğunda toohello kapsayıcı kayıt defteri verilen tooprovide hello benzersiz adı gerekir.

```azurecli
az acr login --name <acrName>
```

Merhaba komut tamamlandıktan sonra 'Başarılı oturum açma' iletisi döndürür.

## <a name="tag-container-image"></a>Etiket kapsayıcı görüntüsü

özel bir kayıt defteri kapsayıcı görüntüden toodeploy, hello görüntü gerekiyor hello ile etiketlenmiş toobe `loginServer` hello kayıt adı.

toosee geçerli görüntüleri, kullanım hello listesini `docker images` komutu.

```bash
docker images
```

Çıktı:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

komutu aşağıdaki hello çalıştırmak tooget hello loginServer adı.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Etiket hello *aci öğretici uygulama* hello loginServer hello kapsayıcı kayıt defteri görüntüsüyle. Ayrıca, ekleme `:v1` toohello adının sonuna kadar hello görüntü. Bu etiket hello görüntü sürüm numarasını gösterir.

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

Etiketlenmiş bir kez çalıştır `docker images` tooverify hello işlemi.

```bash
docker images
```

Çıktı:

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a>Anında iletme görüntü tooAzure kapsayıcı kayıt defteri

Merhaba anında *aci öğretici uygulama* görüntü toohello kayıt defteri.

Aşağıdaki örneğine hello kullanarak, ortamınızdan hello loginServer hello kapsayıcı kayıt defteri loginServer adı değiştirin.

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a>Azure kapsayıcı kayıt defterinde listesi görüntüler

tooreturn tooyour Azure kapsayıcı kayıt defteri, kullanıcı hello gönderilen görüntüleri listesini [az acr deposu listesi](/cli/azure/acr/repository#list) komutu. Merhaba komutu hello kapsayıcı kayıt defteri adıyla güncelleştirin.

```azurecli
az acr repository list --name <acrName> --output table
```

Çıktı:

```azurecli
Result
----------------
aci-tutorial-app
```

Ve ardından belirli bir görüntü için toosee hello etiketler hello [az acr deposunu Göster-etiketleri](/cli/azure/acr/repository#show-tags) komutu.

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

Çıktı:

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide Azure kapsayıcı örnekleri ile kullanmak için bir Azure kapsayıcı kayıt defteri hazırlanan ve hello kapsayıcı görüntü gönderilir. Aşağıdaki adımları hello tamamlandı:

> [!div class="checklist"]
> * Azure kapsayıcı kayıt defteri örneğini dağıtma
> * Azure kapsayıcı kayıt defteri için etiketleme kapsayıcı görüntüsü
> * Görüntü tooAzure kapsayıcı kayıt defteri karşıya yükleme

Azure kapsayıcı örnekleri kullanılarak hello kapsayıcı tooAzure dağıtma hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [Kapsayıcıları tooAzure kapsayıcı örnekleri dağıtma](./container-instances-tutorial-deploy-app.md)
