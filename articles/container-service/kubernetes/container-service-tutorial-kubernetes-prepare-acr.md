---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - hazırlama ACR | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - ACR hazırlama"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Container’lar, Mikro hizmetler, Kumernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Dağıtma ve Azure kapsayıcı kayıt defteri kullanma

Azure kapsayıcı kayıt defteri (ACR) Docker kapsayıcısı görüntüleri için bir Azure tabanlı, özel kayıt defteri ' dir. Bu öğretici, bölümü yedi, iki anlatılmaktadır Azure kapsayıcı kayıt defteri örneğini dağıtma ve kapsayıcı görüntü tooit Ftp'den aracılığıyla. Tamamlanan adımları içerir:

> [!div class="checklist"]
> * Azure kapsayıcı kayıt defteri (ACR) örneğini dağıtma
> * ACR için bir kapsayıcı görüntüsü etiketleme
> * Merhaba görüntü tooACR karşıya yükleme

Sonraki öğreticilerde bu ACR örnek kapsayıcı görüntüleri güvenli bir şekilde çalıştırmak için bir Azure kapsayıcı hizmeti Kubernetes küme tümleşiktir. 

## <a name="before-you-begin"></a>Başlamadan önce

Merhaba, [önceki öğretici](./container-service-tutorial-kubernetes-prepare-app.md), basit bir Azure oylama uygulaması için bir kapsayıcı görüntüsü oluşturuldu. Bu öğreticide, bu görüntüyü tooan Azure kapsayıcı kayıt defteri gönderilir. Hello Azure oylama uygulama görüntüsü oluşturmadıysanız çok dönüş[Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md). Alternatif olarak, hello adımlar burada herhangi bir kapsayıcı görüntü ile çalışma ayrıntılı.

Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırdığınız gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="deploy-azure-container-registry"></a>Azure kapsayıcı kayıt defteri dağıtın

Azure kapsayıcı kayıt defteri dağıtırken, önce bir kaynak grubu gerekir. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Bu örnekte, bir kaynak grubu adında *myResourceGroup* hello oluşturulan *westeurope* bölge.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Azure kapsayıcı kayıt defteri ile Merhaba oluşturma [az acr oluşturmak](/cli/azure/acr#create) komutu. bir kapsayıcı kayıt defteri Hello adını **benzersiz olmalıdır**.

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

Hello rest Bu öğreticinin "acrname" yer tutucu olarak seçtiğiniz hello kapsayıcı kayıt defteri adı için kullanırız.

## <a name="container-registry-login"></a>Kapsayıcı kayıt defteri oturum açma

Görüntüleri tooit göndermeden önce tooyour ACR örneğinde oturum açmanız gerekir. Kullanım hello [az acr oturum açma](https://docs.microsoft.com/en-us/cli/azure/acr#login) toocomplete hello işlemi komutu. Oluşturulduğunda toohello kapsayıcı kayıt defteri verilen tooprovide hello benzersiz adı gerekir.

```azurecli
az acr login --name <acrName>
```

Merhaba komut tamamlandıktan sonra 'Başarılı oturum açma' iletisi döndürür.

## <a name="tag-container-images"></a>Etiket kapsayıcı görüntüleri

Her kapsayıcı görüntü hello loginServer adı hello kayıt defteri ile etiketlenmiş toobe gerekir. Bu etiket kapsayıcı görüntüleri tooan görüntü kayıt defteri Ftp'den zaman yönlendirme için kullanılır.

toosee geçerli görüntüleri, kullanım hello listesini [docker görüntüleri](https://docs.docker.com/engine/reference/commandline/images/) komutu.

```bash
docker images
```

Çıktı:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

komutu aşağıdaki hello çalıştırmak tooget hello loginServer adı.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Şimdi, etiket hello *azure oy ön* hello loginServer hello kapsayıcı kayıt defteri görüntüsüyle. Ayrıca, ekleme `:redis-v1` toohello adının sonuna kadar hello görüntü. Bu etiket hello resim sürümünü gösterir.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

Etiketli sonra [docker görüntüler] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello işlemini çalıştırın.

```bash
docker images
```

Çıktı:

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a>Görüntüleri tooregistry bildirme

Merhaba anında *azure oy ön* görüntü toohello kayıt defteri. 

Aşağıdaki örneğine hello kullanarak, ortamınızdan hello loginServer hello ACR loginServer adı değiştirin.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

Bu işlem birkaç dakika toocomplete götürür.

## <a name="list-images-in-registry"></a>Kayıt defterinde listesi görüntüler

tooreturn tooyour Azure kapsayıcı kayıt defteri, kullanıcı hello gönderilen görüntüleri listesini [az acr deposu listesi](/cli/azure/acr/repository#list) komutu. Merhaba komutu hello ACR örnek adıyla güncelleştirin.

```azurecli
az acr repository list --name <acrName> --output table
```

Çıktı:

```azurecli
Result
----------------
azure-vote-front
```

Ve ardından belirli bir görüntü için toosee hello etiketler hello [az acr deposunu Göster-etiketleri](/cli/azure/acr/repository#show-tags) komutu.

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

Çıktı:

```azurecli
Result
--------
redis-v1
```

Eğitmen tamamlandığında hello kapsayıcı görüntü özel bir Azure kapsayıcı kayıt defteri örneğinde zamandır depolanmış. Bu görüntü ACR tooa Kubernetes kümeden sonraki öğreticilerde dağıtılır.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, bir ACS Kubernetes kümesinde kullanmak için bir Azure kapsayıcı kayıt defteri hazırlanan. Aşağıdaki adımları hello tamamlandı:

> [!div class="checklist"]
> * Azure kapsayıcı kayıt defteri örneği dağıtılan
> * ACR için bir kapsayıcı görüntüsü etiketli
> * Karşıya yüklenen hello görüntü tooACR

Azure Kubernetes kümede dağıtma hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [Kubernetes kümesi dağıtma](./container-service-tutorial-kubernetes-deploy-cluster.md)