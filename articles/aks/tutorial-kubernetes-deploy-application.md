---
title: "Kubernetes Azure Öğreticisi - uygulama dağıtma hakkında"
description: "AKS Öğreticisi - uygulama dağıtma"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 10/24/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 4468424a96b4949161218d495dd21f24285430fd
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/18/2017
---
# <a name="run-applications-in-azure-container-service-aks"></a>Azure kapsayıcı hizmeti (AKS) uygulamaları çalıştırma

Bu öğreticide sekiz dördünü kısım, örnek bir uygulama Kubernetes kümesine dağıtılır. Tamamlanan adımları içerir:

> [!div class="checklist"]
> * Güncelleştirme Kubernetes bildirim dosyaları
> * Kubernetes'te uygulama çalıştırma
> * Uygulamayı test etme

Sonraki öğreticilerde, bu uygulama, güncelleştirilmiş, ölçeklenir ve Kubernetes küme izlemek için Operations Management Suite yapılandırılır.

Bu öğretici Kubernetes kavramlar, Kubernetes bakın hakkında ayrıntılı bilgi için temel bir anlayış varsayar [Kubernetes belgelerine][kubernetes-documentation].

## <a name="before-you-begin"></a>Başlamadan önce

Önceki öğreticileri, bir uygulama bir kapsayıcı görüntüsüne paketlenmiş ve bu görüntüyü Azure kapsayıcı kayıt defterine karşıya Kubernetes küme oluşturuldu. 

Bu öğreticiyi tamamlamak için önceden oluşturulmuş gerekir `azure-vote-all-in-one-redis.yaml` Kubernetes bildirim dosyası. Bu dosya uygulama kaynak koduna bir önceki öğreticide yüklendi. Depoyu kopyalanmış ve kopyalanan deposu dizinleri değiştirilmediğini doğrulayın.

Bu adımları yapmadıysanız ve izlemek istediğiniz, geri dönüp [Öğreticisi 1 – Oluştur kapsayıcı görüntüleri][aks-tutorial-prepare-app].

## <a name="update-manifest-file"></a>Güncelleştirme bildirim dosyası

Bu öğreticide, Azure kapsayıcı kayıt defteri (ACR) bir kapsayıcı görüntüsü depolamak için kullanılmış. Uygulamayı çalıştırmadan önce ACR oturum açma sunucusu adı Kubernetes bildirim dosyasında güncelleştirilmesi gerekiyor.

ACR oturum açma sunucu adıyla alma [az acr listesi] [ az-acr-list] komutu.

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Bildirim dosyası bir oturum açma sunucusu adı ile önceden oluşturulmuş `microsoft`. Dosyayı herhangi bir metin düzenleyicisinde açın. Bu örnekte, dosya içeren açıldıktan `vi`.

```console
vi azure-vote-all-in-one-redis.yaml
```

Değiştir `microsoft` ACR oturum açma sunucu adına sahip. Bu değer satırına bulundu **47** bildirim dosyasının.

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

Dosyasını kaydedin ve kapatın.

## <a name="deploy-application"></a>Uygulama dağıtma

Kullanım [kubectl oluşturma] [ kubectl-create] uygulamayı çalıştırmak için komutu. Bu komut, bildirim dosyası ayrıştırır ve tanımlanmış Kubernetes nesneleri oluşturur.

```azurecli
kubectl create -f azure-vote-all-in-one-redis.yaml
```

Çıktı:

```
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a>Uygulamayı test etme

A [Kubernetes hizmet] [ kubernetes-service] hangi uygulamanın Internet'e gösterir oluşturulur. Bu işlem birkaç dakika sürebilir. 

İlerleme durumunu izlemek için kullanın [kubectl alma hizmeti] [ kubectl-get] komutunu `--watch` bağımsız değişkeni.

```azurecli
kubectl get service azure-vote-front --watch
```

Başlangıçta *azure-vote-front* için *EXTERNAL-IP* durumu *pending* olarak görünür.
  
```
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
```

*EXTERNAL-IP* adresi *pending* durumundan *IP address* değerine değiştiğinde kubectl izleme işlemini durdurmak için `CTRL-C` komutunu kullanın. 

```
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

Uygulama görmek için dış IP adresine göz atın.

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, Azure oy uygulama AKS Kubernetes kümede için dağıtıldı. Tamamlanan görevler aşağıdakileri içerir:  

> [!div class="checklist"]
> * Kubernetes bildirim dosyaları indirme
> * İçinde Kubernetes uygulamayı çalıştırın
> * Uygulamayı test

Kubernetes uygulama ve Kubernetes altyapının ölçeklendirme hakkında bilgi edinmek için sonraki öğretici ilerleyin. 

> [!div class="nextstepaction"]
> [Ölçek Kubernetes uygulama ve altyapı][aks-tutorial-scale]

<!-- LINKS - external -->
[kubectl-create]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubernetes-documentation]: https://kubernetes.io/docs/home/
[kubernetes-service]: https://kubernetes.io/docs/concepts/services-networking/service/

<!-- LINKS - internal -->
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
[aks-tutorial-scale]: ./tutorial-kubernetes-scale.md
[az-acr-list]: /cli/azure/acr#list
