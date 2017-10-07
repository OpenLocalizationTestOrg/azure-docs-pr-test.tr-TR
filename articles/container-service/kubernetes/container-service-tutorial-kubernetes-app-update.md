---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - güncelleştirme uygulaması | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - güncelleştirme uygulaması"
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
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a>Bir uygulamada Kubernetes güncelleştir

Bir uygulamada Kubernetes dağıttıktan sonra yeni kapsayıcı resim veya görüntü sürümü belirterek güncelleştirilebilir. Bir uygulama'ı güncelleştirdiğinizde hello güncelleştirme dağıtımının hello dağıtım yalnızca bir kısmını eşzamanlı olarak güncelleştirilebilmesi için hazırdır. Hazırlanan bu güncelleştirmeyi hello güncelleştirme sırasında çalışan hello uygulama tookeep sağlar ve bir dağıtım hatası oluşursa, bir geri alma mekanizması sağlar. 

Bu öğreticide, yedi, hello örnek Azure oylama uygulaması altı parçası güncelleştirilir. Tamamlamanız görevler aşağıdakileri içerir:

> [!div class="checklist"]
> * Merhaba ön uç uygulamasındaki kod güncelleştiriliyor
> * Güncelleştirilmiş kapsayıcı görüntü oluşturma
> * Koymadan hello kapsayıcı görüntü tooAzure kapsayıcı kayıt defteri
> * Merhaba güncelleştirilmiş kapsayıcı görüntü dağıtma

Sonraki öğreticilerde Operations Management Suite yapılandırılmış toomonitor hello Kubernetes kümedir.

## <a name="before-you-begin"></a>Başlamadan önce

Önceki öğreticileri, bir uygulama bir kapsayıcı görüntüsüne paketlenmiş, tooAzure kapsayıcı kayıt defteri ve oluşturulan Kubernetes küme hello görüntüyü karşıya. Merhaba uygulaması sonra hello Kubernetes kümede çalıştırıldı. 

Bu adımları tamamladıysanız henüz ve boyunca toofollow istediğiniz çok dönmek[Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md). 

## <a name="update-application"></a>Uygulamayı güncelleştirme

toocomplete hello adımları Bu öğreticide, hello Azure oy uygulama kopyasını kopyalanmış gerekir. Gerekirse, kopyalanan bu kopya komut aşağıdaki hello ile oluşturun:

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Açık hello `config_file.cfg` herhangi bir kod ya da metin düzenleyicisi ile dosya. Bu dosyayı klonlanmış hello deposu dizinini aşağıdaki hello altında bulabilirsiniz.

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

Değiştirmek için hello değerleri `VOTE1VALUE` ve `VOTE2VALUE`ve hello dosyasını kaydedin.

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

Kullanım [docker compose'u](https://docs.docker.com/compose/) toore-hello ön uç görüntü ve güncelleştirilmiş çalışma Merhaba uygulaması oluşturun.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a>Uygulamayı yerel olarak test etme

Çok Gözat`http://localhost:8080` toosee hello uygulama güncelleştirildi.

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a>Etiket ve anında iletme görüntüleri

Etiket hello *azure oy ön* hello loginServer hello kapsayıcı kayıt defteri görüntüsüyle.

Azure kapsayıcı kayıt defteri kullanıyorsanız, hello hello oturum açma sunucu adıyla alma [az acr listesi](/cli/azure/acr#list) komutu.

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Kullanım [docker etiketi](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello görüntü. Değiştir `<acrLoginServer>` Azure kapsayıcı kayıt defteri oturum açma sunucu adı veya ortak kayıt defteri ana bilgisayar adı.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

Kullanım [docker itme](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello görüntü tooyour kayıt defteri. Değiştir `<acrLoginServer>` Azure kapsayıcı kayıt defteri oturum açma sunucu adı veya ortak kayıt defteri ana bilgisayar adı.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a>Güncelleştirme uygulaması dağıtma

tooensure en fazla çalışma süresi, birden çok örneğini hello uygulama pod çalıştırması gerekir. Bu yapılandırma ile Merhaba doğrulayın [kubectl alma pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu.

```bash
kubectl get pod
```

Çıktı:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

Birden çok pod'ları hello azure oy ön görüntüsünü çalıştıran yoksa, hello ölçeklendirme *azure oy ön* dağıtım.


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

tooupdate Merhaba uygulaması, kullanım hello [kubectl kümesi](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) komutu. Güncelleştirme `<acrLoginServer>` hello oturum açma sunucusu veya ana bilgisayar adı, kapsayıcı kayıt defteri.

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

toomonitor hello dağıtım, kullanım hello [kubectl alma pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu. Güncelleştirilmiş hello uygulamanın dağıtıldığını gibi pod'ları sonlandırıldı ve hello yeni kapsayıcı görüntüsü ile yeniden oluşturulacak.

```azurecli-interactive
kubectl get pod
```

Çıktı:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a>Güncelleştirilmiş uygulamayı test etme

Merhaba Hello dış IP adresi al *azure oy ön* hizmet.

```azurecli-interactive
kubectl get service azure-vote-front
```

Gözat toohello IP adresi toosee hello uygulama güncelleştirildi.

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, bir uygulamanın güncelleştirilmiş ve bu güncelleştirme tooa Kubernetes küme alındı. görevleri aşağıdaki hello tamamlandı:

> [!div class="checklist"]
> * Güncelleştirilmiş hello ön uç uygulamasındaki kod
> * Güncelleştirilmiş kapsayıcı görüntüyü oluşturuldu
> * Merhaba kapsayıcı görüntü tooAzure kapsayıcı kayıt defteri gönderilir
> * Dağıtılan hello güncelleştirilmiş uygulama

İlerlemek toohello sonraki öğretici toolearn konusunda toomonitor Kubernetes Operations Management Suite ile.

> [!div class="nextstepaction"]
> [OMS ile Kubernetes’i izleme](./container-service-tutorial-kubernetes-monitor.md)