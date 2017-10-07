---
title: "bir Azure Kubernetes aaaMonitor CoScale ile küme | Microsoft Docs"
description: "İzleyici CoScale kullanarak Azure kapsayıcı hizmeti Kubernetes kümede"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a>Azure kapsayıcı hizmeti Kubernetes küme CoScale ile izleme

Bu makalede, nasıl gösteriyoruz toodeploy hello [CoScale](https://www.coscale.com/) tüm düğümler ve, Kubernetes kapsayıcılarında Azure kapsayıcı Hizmeti'nde küme Aracısı toomonitor. Bu yapılandırma için CoScale sahip bir hesap gerekir. 


## <a name="about-coscale"></a>CoScale hakkında 

CoScale birkaç orchestration platformlarda tüm kapsayıcıları gelen ölçümleri ve olayları toplayan izleme bir platformdur. CoScale Kubernetes ortamlar için tam yığını izleme sunar. Merhaba yığınındaki tüm katmanlar için görselleştirme ve analizi sağlar: işletim sistemi, Kubernetes, Docker ve kapsayıcıların içinde çalışan uygulamaların hello. Birkaç yerleşik izleme panoları, coScale sunar ve yerleşik anomali algılama tooallow işleçleri sahiptir ve geliştiricilerin toofind altyapı ve uygulama sorunlarını hızlı.

![UI coScale](./media/container-service-kubernetes-coscale/coscale.png)

Bu makalede gösterildiği gibi aracıları Kubernetes küme toorun CoScale bir SaaS çözümü olarak yükleyebilirsiniz. Verilerinizi şirkete tookeep istiyorsanız CoScale de şirket içi yükleme için kullanılabilir.


## <a name="prerequisites"></a>Ön koşullar

İlk çok gereksinim[CoScale hesabı oluşturma](https://www.coscale.com/free-trial).

Bu kılavuz, sahibi olduğunuzu varsayar [Azure kapsayıcı hizmeti kullanarak Kubernetes küme oluşturulan](container-service-kubernetes-walkthrough.md).

Ayrıca, hello sahibi olduğunuzu varsayar `az` Azure CLI ve `kubectl` araçları yüklü.

Merhaba varsa test edebilirsiniz `az` çalıştırarak yüklü aracı:

```azurecli
az --version
```

Merhaba yoksa `az` yüklü, aracı yönergeler vardır [burada](/cli/azure/install-azure-cli).

Merhaba varsa test edebilirsiniz `kubectl` çalıştırarak yüklü aracı:

```bash
kubectl version
```

Sahip değilseniz `kubectl` yüklü çalıştırabilirsiniz:

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a>DaemonSet ile Merhaba CoScale Aracısı yükleniyor
[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) olan hello kümedeki her ana bilgisayarda bir kapsayıcı tek bir örneğini Kubernetes toorun tarafından kullanılır.
Bunlar hello CoScale aracı gibi izleme aracıları çalıştırmak için mükemmel.

İçinde tooCoScale oturum sonra toohello gidin [Aracısı sayfası](https://app.coscale.com/) tooinstall CoScale aracıları bir DaemonSet kullanarak kümenizde. Merhaba CoScale UI destekli yapılandırma adımları toocreate bir aracı ve başlangıç tam Kubernetes kümenizi izleme sağlar.

![CoScale Aracısı yapılandırması](./media/container-service-kubernetes-coscale/installation.png)

toostart hello Aracısı hello kümede sağlanan hello komutu çalıştırın:

![Merhaba CoScale aracısını başlatın](./media/container-service-kubernetes-coscale/agent_script.png)

İşte bu kadar! Merhaba aracıları ve çalışıyor olduktan sonra birkaç dakika içinde veri hello konsolunda görmeniz gerekir. Merhaba ziyaret [Aracısı sayfası](https://app.coscale.com/) toosee kümenizde özetini ek yapılandırma adımları uygulayın ve panolar hello gibi bkz **Kubernetes küme genel bakış**.

![Kubernetes küme genel bakış](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

Merhaba CoScale Aracısı hello kümedeki yeni makinelere otomatik olarak dağıtılır. otomatik olarak yeni bir sürümü yayımlandığında hello aracı güncelleştirmeleri.


## <a name="next-steps"></a>Sonraki adımlar

Merhaba bkz [CoScale belgelerine](http://docs.coscale.com/) ve [blog](https://www.coscale.com/blog) CoScale çözümlerini izleme hakkında daha fazla bilgi için. 

