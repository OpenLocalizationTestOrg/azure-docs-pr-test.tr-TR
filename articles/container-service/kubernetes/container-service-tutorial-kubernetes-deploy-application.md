---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - uygulama dağıtma | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - uygulama dağıtma"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Container’lar, Mikro hizmetler, Kumernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a>Kubernetes çalışma uygulamaları

Bu öğreticide yedi dördünü kısım, örnek bir uygulama Kubernetes kümesine dağıtılır. Tamamlanan adımları içerir:

> [!div class="checklist"]
> * Kubernetes bildirim dosyaları indirme
> * Kubernetes Çalıştırma uygulaması
> * Merhaba uygulamayı test etme

Sonraki öğreticilerde, bu uygulama, güncelleştirilmiş, ölçeklenir ve Operations Management Suite toomonitor hello Kubernetes küme yapılandırılır.

Bu öğretici Kubernetes kavramları temel bir anlayış varsayar, hello Kubernetes hakkında ayrıntılı bilgi için bkz: [Kubernetes belgelerine](https://kubernetes.io/docs/home/).

## <a name="before-you-begin"></a>Başlamadan önce

Önceki öğreticileri, bir uygulama bir kapsayıcı görüntüsüne paketlenmiş ve bu görüntüyü karşıya yüklenen tooAzure kapsayıcı kayıt defteri edildi Kubernetes küme oluşturuldu. Bu adımları yapmadıysanız ve boyunca toofollow istersiniz, çok dönmek[Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md). 

En azından, Bu öğretici Kubernetes kümesi gerektirir.

## <a name="get-manifest-file"></a>Bildirim dosyası al

Bu öğretici için [Kubernetes nesneleri](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) Kubernetes bildirimi kullanılarak dağıtılır. Kubernetes bildirim Kubernetes nesne dağıtım ve yapılandırma yönergeleri içeren bir YAML veya JSON biçimli dosyasıdır.

önceki bir öğreticide kopyalandı hello Azure oy uygulama depodaki Hello uygulama bildirim dosyasının Bu öğretici için kullanılabilir. Zaten yapmadıysanız, komutu aşağıdaki hello ile Merhaba depoyu kopyalama: 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

kopyalanmış hello deposu dizinini aşağıdaki hello Hello bildirim dosyası bulunamadı.

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a>Güncelleştirme bildirim dosyası

Azure kapsayıcı kayıt defteri toostore hello kapsayıcı görüntüleri kullanıyorsanız, hello bildirim gereksinimlerini toobe ACR loginServer adı ile Merhaba güncelleştirildi.

Merhaba ACR oturum açma sunucu hello adıyla alma [az acr listesi](/cli/azure/acr#list) komutu.

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Merhaba örnek bildirimi bir havuz adı ile önceden oluşturulmuş *microsoft*. Merhaba dosya ile herhangi bir metin düzenleyicisinde açın ve hello değiştirin *microsoft* hello oturum açma sunucusu adlı ACR örneğinin değeri.

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a>Uygulama dağıtma

Kullanım hello [kubectl oluşturma](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) toorun Merhaba uygulaması komutu. Bu komut ayrıştırıyor hello bildirim dosyası ve tanımlanan hello Kubernetes nesneleri oluşturun.

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

Çıktı:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a>Uygulamayı test etme

A [Kubernetes hizmet](https://kubernetes.io/docs/concepts/services-networking/service/) hangi hello uygulama toohello sunan oluşturulan Internet. Bu işlem birkaç dakika sürebilir. 

toomonitor ilerleme, kullanım hello [kubectl alma hizmeti](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) hello komutunu `--watch` bağımsız değişkeni.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

Başlangıçta, hello **dış IP** hello için *azure oy ön* hizmeti görünür olarak *bekleyen*. Merhaba dış IP adresi değiştiğinden sonra *bekleyen* tooan *IP adresi*, kullanın `CTRL-C` toostop hello kubectl izleme işlemi.

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

toosee Merhaba uygulaması, Gözat toohello dış IP adresi.

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, dağıtılan tooan Azure kapsayıcı hizmeti Kubernetes küme hello Azure oy uygulama oluştu. Tamamlanan görevler aşağıdakileri içerir:  

> [!div class="checklist"]
> * Kubernetes bildirim dosyaları indirme
> * İçinde Kubernetes Hello uygulamayı çalıştırın
> * Sınanan Merhaba uygulaması

Bir Kubernetes uygulama ve Kubernetes altyapısını temel hello ölçeklendirme hakkında toohello sonraki öğretici toolearn ilerleyin. 

> [!div class="nextstepaction"]
> [Ölçek Kubernetes uygulama ve altyapı](./container-service-tutorial-kubernetes-scale.md)