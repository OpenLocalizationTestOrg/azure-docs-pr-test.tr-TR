---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - uygulamayı Ölçeklendir | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - uygulamayı Ölçeklendir"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Mikro docker, kapsayıcıları, hizmetleri, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a>Ölçek Kubernetes pod'ları ve Kubernetes altyapısı

Hello öğreticileri takip, Azure kapsayıcı Hizmeti'nde çalışan Kubernetes küme sahip olmanız ve hello Azure oylama uygulaması dağıtılır. 

Bu öğreticide parçası beş yedi, hello pod'ları hello uygulamasında ölçeğini ve pod otomatik ölçeklendirmeyi deneyin. Ayrıca, nasıl Azure VM Aracısı düğümleri toochange tooscale hello sayısı hello iş yüklerini barındırmak için kümenin kapasite öğrenin. Tamamlanan görevler aşağıdakileri içerir:

> [!div class="checklist"]
> * Kubernetes pod'ları el ile ölçeklendirme
> * Merhaba uygulaması ön ucu çalıştıran otomatik ölçeklendirme pod'ları yapılandırma
> * Merhaba Kubernetes Azure Aracısı düğümleri ölçeklendirme

Sonraki öğreticilerde, hello Azure oy uygulama güncelleştirilir ve Operations Management Suite toomonitor hello Kubernetes kümesi yapılandırılır.

## <a name="before-you-begin"></a>Başlamadan önce

Önceki öğreticileri, bir uygulama bir kapsayıcı görüntüsüne paketlenmiş, tooAzure kapsayıcı kayıt defteri ve oluşturulan bir Kubernetes kümesi bu görüntüyü karşıya. Merhaba uygulaması sonra hello Kubernetes kümede çalıştırıldı. Bu adımları yapmadıysanız ve boyunca toofollow istersiniz, toohello dönmek [Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md). 

En azından, Bu öğretici bir Kubernetes kümesi ile çalışan bir uygulama gerektirir.

## <a name="manually-scale-pods"></a>Pod'ları el ile ölçeklendirin

Bugüne kadarki hello Azure oy ön uç ve Redis örnek dağıtıldıktan, her tek bir çoğaltma ile. Merhaba çalıştırmak tooverify [kubectl almak](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu.

```azurecli-interactive
kubectl get pods
```

Çıktı:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

El ile pod'ları hello içinde hello sayısını değiştirme `azure-vote-front` hello kullanarak dağıtım [kubectl ölçek](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) komutu. Bu örnek hello numara too5 artırır.

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

Çalıştırma [kubectl pod'ları alma](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify Kubernetes hello pod'ları oluşturuyor. Bir dakika veya bunu sonra ek hello pod'ları çalıştırıyorsanız:

```azurecli-interactive
kubectl get pods
```

Çıktı:

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a>Otomatik ölçeklendirme pod'ları

Kubernetes destekleyen [yatay pod otomatik ölçeklendirmeyi](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello pod'ları CPU kullanımı veya diğer bağlı olarak bir dağıtımda sayısını ölçümleri seçin. 

toouse hello autoscaler, pod'ları CPU istekleri ve sınırları tanımlanmış olması gerekir. Merhaba, `azure-vote-front` dağıtımı, ön uç kapsayıcı istekleri 0,25 CPU 0,5 sınırı ile Merhaba CPU. gibi Hello ayarlarını arayın:

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

Merhaba aşağıdaki örnek kullanır hello [kubectl otomatik ölçeklendirme](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) komut tooautoscale hello pod'ları hello içinde sayısı `azure-vote-front` dağıtım. Burada, CPU kullanımı % 50 aşarsa hello autoscaler hello pod'ları tooa en fazla 10 artırır.


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

Merhaba autoscaler, komutu aşağıdaki hello çalıştırmak toosee hello durumu:

```azurecli-interactive
kubectl get hpa
```

Çıktı:

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

Merhaba pod çoğaltmaların sayısı hello Azure oy uygulama üzerinde minimum yük ile birkaç dakika sonra otomatik olarak too3 azaltır.

## <a name="scale-hello-agents"></a>Ölçek hello aracıları

Merhaba önceki öğreticide varsayılan komutlarını kullanarak Kubernetes kümenize oluşturduysanız, üç Aracısı düğüm yok. Daha fazla veya daha az sayıda kapsayıcı iş yükleri kümenizde düşünüyorsanız, aracı hello sayısı el ile ayarlayabilirsiniz. Kullanım hello [az acs ölçeklendirme](/cli/azure/acs#scale) komutu ve aracı hello sayısı ile Merhaba belirtin `--new-agent-count` parametresi.

Merhaba aşağıdaki örnek hello sayısını Aracısı düğümleri too4 adlı hello Kubernetes kümedeki artırır *myK8sCluster*. birkaç dakika toocomplete Hello komutu alır.

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

Merhaba komutu çıktısı hello sayısını Aracısı düğümleri hello değerinde gösterir `agentPoolProfiles:count`:

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, farklı ölçekleme özelliklerini Kubernetes kümenizdeki kullanılır. Görevleri dahil ele:

> [!div class="checklist"]
> * Kubernetes pod'ları el ile ölçeklendirme
> * Merhaba uygulaması ön ucu çalıştıran otomatik ölçeklendirme pod'ları yapılandırma
> * Merhaba Kubernetes Azure Aracısı düğümleri ölçeklendirme

Kubernetes uygulamada güncelleştirme hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [Bir uygulamada Kubernetes güncelleştir](./container-service-tutorial-kubernetes-app-update.md)

