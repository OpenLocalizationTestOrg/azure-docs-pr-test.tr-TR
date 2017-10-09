---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - İzleyici Kubernetes | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - İzleyici Kubernetes Microsoft Operations Management Suite (OMS)"
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
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a>Operations Management Suite Kubernetes kümeyle izleme

Özellikle birden çok uygulama ile ölçekli üretim kümesi yönetirken izleme Kubernetes küme ve kapsayıcıları, önemlidir. 

Birkaç Kubernetes izleme çözümlerinin, Microsoft veya diğer sağlayıcıları avantajından yararlanabilirsiniz. Bu öğreticide, Kubernetes kümenizi Merhaba kapsayıcılara çözümde kullanarak izlemenizi [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft'un bulut tabanlı BT yönetim çözümü. (Merhaba OMS kapsayıcıları çözüm önizlemede değil.)

Bu öğretici, parçası yedi yedi, görevleri aşağıdaki hello kapsar:

> [!div class="checklist"]
> * OMS çalışma ayarlarını al
> * Merhaba Kubernetes düğümlerdeki OMS aracılarını ayarlama
> * İzleme bilgilerini hello OMS portalında veya Azure portalına erişim

## <a name="before-you-begin"></a>Başlamadan önce

Önceki öğreticileri, bir uygulama kapsayıcı görüntülere paketlenmiş, bu görüntüleri tooAzure kapsayıcı kayıt defteri ve oluşturulan Kubernetes küme karşıya. Bu adımları yapmadıysanız ve boyunca toofollow istersiniz, çok dönmek[Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md). 

En azından, Bu öğretici Linux Aracısı düğümleri ve bir Operations Management Suite (OMS) hesap Kubernetes kümeyle gerektirir. Gerekirse, kaydolun bir [ücretsiz OMS deneme](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).

## <a name="get-workspace-settings"></a>Çalışma alanı ayarlarını al

Ne zaman erişebilirsiniz hello [OMS portalı](https://mms.microsoft.com), çok Git**ayarları** > **bağlı kaynakları** > **Linux sunucuları**. Merhaba, bulabilirsiniz *çalışma alanı kimliği* ve birincil veya ikincil *çalışma alanı anahtarı*. Gereksinim duyduğunuz bu değerleri not edin tooset hello kümede OMS Aracısı ayarlama.

## <a name="set-up-oms-agents"></a>OMS aracılarını ayarlama

Burada, OMS Aracısı hello Linux küme düğümlerinde yukarı YAML dosya tooset verilmiştir. Bir Kubernetes oluşturur [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), her küme düğümünde tek aynı pod çalıştırır. Merhaba DaemonSet kaynak izleme aracısını dağıtmak için idealdir. 

Aşağıdaki metin tooa dosyasına adlı hello Kaydet `oms-daemonset.yaml`ve hello yer tutucu değerlerini değiştirme *myWorkspaceID* ve *myWorkspaceKey* OMS çalışma alanı kimliği ve anahtarı. (Üretimde, bu değerleri gizlilikleri olarak şifreleyebilirsiniz.)

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

Merhaba DaemonSet komutu aşağıdaki hello ile oluşturun:

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

toosee DaemonSet oluşturulur, bu hello çalıştırın:

```azurecli-interactive
kubectl get daemonset
```

Çıktı benzer toohello aşağıda verilmiştir:

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

Merhaba aracılar çalışan sonra OMS tooingest ve işlem hello veriler için birkaç dakika sürer.

## <a name="access-monitoring-data"></a>İzleme verilerine erişim

Görüntüleme ve hello OMS kapsayıcı hello verilerle izleme çözümleme [kapsayıcı çözüm](../../log-analytics/log-analytics-containers.md) hello OMS portalında veya hello Azure portalı. 

Hello kullanarak tooinstall hello kapsayıcı çözüm [OMS portalı](https://mms.microsoft.com), çok Git**Çözümleri Galerisi**. Ardından ekleyin **kapsayıcı çözüm**. Alternatif olarak, hello Merhaba kapsayıcılara Çözüm Ekle [Azure Marketi](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).

Merhaba OMS portalında aramak bir **kapsayıcıları** hello OMS Pano Özet kutucuğu. Gibi ayrıntıları Hello kutucuğa tıklayın: kapsayıcı olayları, hatalar, durumu, görüntü stok ve CPU ve bellek kullanımı. Daha ayrıntılı bilgi için herhangi bir kutucuğu satırındaki'ı tıklatın veya gerçekleştirmek bir [günlük arama](../../log-analytics/log-analytics-log-searches.md).

![OMS portalında kapsayıcıları Panosu](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

Benzer şekilde, çok hello Azure portal, Git**günlük analizi** ve çalışma alanı adı seçin. toosee hello **kapsayıcıları** Özet kutucuğuna tıklayın **çözümleri** > **kapsayıcıları**. toosee Ayrıntılar hello kutucuğu'ı tıklatın.

Merhaba bkz [Azure günlük analizi belgeleri](../../log-analytics/index.md) sorgulama ve izleme verilerini analiz etme konusunda ayrıntılı yönergeler için.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, OMS Kubernetes kümenizle izlenen. Görevleri dahil ele:

> [!div class="checklist"]
> * OMS çalışma ayarlarını al
> * Merhaba Kubernetes düğümlerdeki OMS aracılarını ayarlama
> * İzleme bilgilerini hello OMS portalında veya Azure portalına erişim


Kod örnekleri için kapsayıcı hizmeti önceden oluşturulmuş Bu bağlantı toosee izleyin.

> [!div class="nextstepaction"]
> [Azure kapsayıcı hizmeti kod örnekleri](cli-samples.md)
