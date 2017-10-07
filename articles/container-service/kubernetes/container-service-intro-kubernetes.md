---
title: "aaaIntroduction tooAzure Kubernetes için kapsayıcı hizmeti | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Kubernetes için basit toodeploy kolaylaştırır ve Azure kapsayıcı tabanlı uygulamayı yönetin."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes, Docker, Kapsayıcılar, Mikro Hizmetler, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a>Giriş tooAzure Kubernetes için kapsayıcı hizmeti
Azure kapsayıcı hizmeti Kubernetes için basit toocreate kolaylaştırır, yapılandırabilir ve küme sanal makinelerin kapsayıcılı önceden yapılandırılmış toorun uygulamaları yönetebilirsiniz. Bu, toouse varolan yeteneklerinizi sağlar veya topluluk uzmanlık toodeploy büyük ve artan gövde çizme ve Microsoft Azure üzerinde kapsayıcı tabanlı uygulamalar yönetin.

Azure kapsayıcı hizmeti kullanarak, hello Azure, kurumsal düzeyde özelliklerini hala Kubernetes aracılığıyla uygulama taşınabilirliği korurken yararlanmak ve Docker görüntü biçimi hello.

## <a name="using-azure-container-service-for-kubernetes"></a>Kubernetes için Azure Container Service’i Kullanma
Amacımız Azure kapsayıcı hizmeti ile tooprovide bir kapsayıcı barındırma ortamı açık kaynaklı araçları ve bugün müşterilerimizin arasında popüler teknolojileri kullanmaktır. toothis son biz hello standart Kubernetes API uç noktalarını kullanıma sunar. Bu standart uç noktaları kullanarak tooa Kubernetes küme Konuşmayı yeteneğine sahip herhangi bir yazılım yararlanabilirsiniz. Örneğin [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) veya [draft](https://github.com/Azure/draft) arasından seçim yapabilirsiniz.

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a>Azure Container Service kullanan bir Kubernetes kümesi oluşturma
Azure kapsayıcı hizmeti kullanarak toobegin hello ile Azure kapsayıcı hizmeti kümesini dağıtma [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) veya hello Portalı aracılığıyla (arama hello Market için **Azure kapsayıcı hizmeti**). Hello Azure Resource Manager şablonları hakkında daha fazla denetime gereksinim duyan İleri düzey bir kullanıcı varsa, hello açık kaynak kullanabilirsiniz [acs altyapısı](https://github.com/Azure/acs-engine) proje toobuild kendi özel Kubernetes küme ve hello dağıtma `az` CLI.

### <a name="using-kubernetes"></a>Kubernetes kullanma
Kubernetes, kapsayıcılı uygulamaların dağıtımını, ölçeklendirmesini ve yönetimini otomatikleştirir. Aşağıdaki zengin özelliklere sahiptir:
* Otomatik bin paketleme
* Kendi kendini iyileştirme
* Yatay ölçekleme
* Hizmet bulma ve yük dengeleme
* Otomatik piyasaya çıkarma ve geri alma işlemleri
* Gizli dizi ve yapılandırma yönetimi
* Depolama düzenleme
* Toplu iş yürütme

Azure Container Service aracılığıyla dağıtılan Kubernetes mimari diyagramı:

![Azure kapsayıcı hizmeti toouse Kubernetes yapılandırılmış.](media/acs-intro/kubernetes.png)

## <a name="videos"></a>Videolar

Azure Container Services'daki Kubernetes Desteği (Azure Friday, Ocak 2017):

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

Kubernetes’te Uygulama Geliştirme ve Dağıtma Araçları (Azure OpenDev, Haziran 2017):

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a>Sonraki adımlar

Merhaba keşfedin [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) Azure kapsayıcı hizmeti bugün keşfetme toobegin.
