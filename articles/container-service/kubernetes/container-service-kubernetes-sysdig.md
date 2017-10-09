---
title: "aaaMonitor Azure Kubernetes küme - Sysdig | Microsoft Docs"
description: "Kubernetes Sysdig kullanarak Azure kapsayıcı hizmeti kümesinde izleme"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a>Sysdig kullanarak Azure kapsayıcı hizmeti Kubernetes küme izleme

## <a name="prerequisites"></a>Ön koşullar
Bu kılavuz, sahibi olduğunuzu varsayar [Azure kapsayıcı hizmeti kullanarak Kubernetes küme oluşturulan](container-service-kubernetes-walkthrough.md).

Hello azure CLI ve kubectl araçlarının yüklü olduğunu varsayar.

Merhaba varsa test edebilirsiniz `az` çalıştırarak yüklü aracı:

```console
$ az --version
```

Merhaba yoksa `az` yüklü, aracı yönergeler vardır [burada](https://github.com/azure/azure-cli#installation).

Merhaba varsa test edebilirsiniz `kubectl` çalıştırarak yüklü aracı:

```console
$ kubectl version
```

Sahip değilseniz `kubectl` yüklü çalıştırabilirsiniz:

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a>Sysdig
Bir dış Azure'da çalışan Kubernetes kümenizi kapsayıcılarında izleyebilirsiniz bir hizmet şirket olarak izleme Sysdig olur. Sysdig kullanarak etkin bir Sysdig hesabı gerektirir.
İçin bir hesap üzerinde kaydolabilirsiniz kendi [site](https://app.sysdigcloud.com).

Toohello Sysdig bulut Web sitesinde oturum açtınız sonra kullanıcı adına tıklayın ve hello sayfasında "Erişim anahtarınızı." görmeniz gerekir 

![Sysdig API anahtarı](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a>Merhaba Sysdig aracıları tooKubernetes yükleme
Her bir işlemi Sysdig çalışır kapsayıcılarınızı makine bir Kubernetes kullanarak toomonitor `DaemonSet`.
DaemonSets bir kapsayıcı makine başına tek bir örneğini çalıştıran Kubernetes API nesneleridir.
Bunlar Sysdig'ın İzleme Aracısı hello gibi araçlar yüklemek için mükemmel.

tooinstall hello Sysdig daemonset ilk karşıdan [hello şablonu](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) sysdig gelen. Bu dosya olarak kaydetmek `sysdig-daemonset.yaml`.

Linux ve OS X çalıştırabilirsiniz:

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

PowerShell içinde:

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

Ardından bu dosya tooinsert erişim Sysdig hesabınızdan aldığınız anahtarınız, düzenleyin.

Son olarak, hello DaemonSet oluşturun:

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a>İzlemenizi görüntüleyin
Yüklü ve çalışır sonra hello aracıları veri geri tooSysdig pompa.  Toothe dönün [sysdig Pano](https://app.sysdigcloud.com) ve kapsayıcıları hakkında bilgiler görmeniz gerekir.

Kubernetes özel panolar aracılığıyla da yükleyebilirsiniz [yeni pano Sihirbazı'nı](https://app.sysdigcloud.com/#/dashboards/new).
