---
title: "aaaMonitor bir Azure kapsayıcı hizmeti kümesi ile Sysdig | Microsoft Docs"
description: "Sysdig ile bir Azure Container Service kümesini izleyin."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Sysdig ile bir Azure Container Service kümesini izleme
Bu makalede, sizi Azure kapsayıcı hizmeti kümenizdeki Sysdig aracıları tooall hello Aracısı düğümlerin dağıtır. Bu yapılandırma için bir Sysdig hesabınızın olması gerekir. 

## <a name="prerequisites"></a>Ön koşullar
Azure Container Service tarafından yapılandırılmış bir kümeyi [dağıtın](container-service-deployment.md) ve [bağlayın](../container-service-connect.md). Merhaba keşfedin [Marathon kullanıcı Arabirimi](container-service-mesos-marathon-ui.md). Çok Git[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset Sysdig bulut hesabı. 

## <a name="sysdig"></a>Sysdig
Sysdig olan toomonitor sağlayan bir izleme hizmeti, kümenizi kapsayıcılara. Sorun giderme toohelp Sysdig bilinir ancak aynı zamanda temel izleme ölçümlerinizi CPU, ağ, bellek ve g/ç için bulunur. Sysdig kapsayıcıları çalıştığınız kolay toosee kılar hardest veya temelde kullanarak hello hello çoğu bellek ve CPU. Merhaba, "şu an beta genel bakış" bölümünde, bu görünüm kullanılıyor. 

![Sysdig Kullanıcı Arabirimi](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Marathon ile bir Sysdig dağıtımı yapılandırma
Bu adımlar şunları nasıl yapacağınızı gösterilecek tooconfigure ve Sysdig uygulamaları tooyour küme Marathon ile dağıtın. 

DC/OS kullanıcı Arabirimi aracılığıyla erişim [http://localhost:80 /](http://localhost:80/) kez hello DC/OS kullanıcı Arabirimi hello üzerinde olan "Universe" sol alt ve "Sysdig" için arama toohello gidin

![DC/OS Evreninde Sysdig](./media/container-service-monitoring-sysdig/sysdig1.png)

Şimdi, bir Sysdig gerek toocomplete hello yapılandırma hesap veya ücretsiz bir deneme hesabı bulut. Toohello Sysdig bulut Web sitesinde oturum açtınız sonra kullanıcı adına tıklayın ve hello sayfasında "Erişim anahtarınızı." görmeniz gerekir 

![Sysdig API anahtarı](./media/container-service-monitoring-sysdig/sysdig2.png) 

Sonraki hello Sysdig yapılandırma hello DC/OS Universe içinde uygulamasına erişim anahtarınızı girin. 

![Merhaba DC/OS Universe Sysdig yapılandırma](./media/container-service-monitoring-sysdig/sysdig3.png)

Şimdi yeni bir düğüm eklendiğinde toohello küme Sysdig otomatik olarak bir aracı dağıtmak için hello örnekleri too10000000 toothat yeni düğüm kümesi. Bu, bir geçici çözüm toomake Sysdig tooall yeni hello küme aracılarına dağıtacağınız emin olur. 

![Merhaba DC/OS Universe-örnekleri Sysdig yapılandırma](./media/container-service-monitoring-sysdig/sysdig4.png)

Merhaba paketini yükledikten sonra geri toohello Sysdig UI gidin ve küme içinde Merhaba kapsayıcılara için mümkün tooexplore hello farklı kullanım ölçümleri olması. 

Ayrıca [yeni pano sihirbazıyla](https://app.sysdigcloud.com/#/dashboards/new) Mesos ve Marathon'a özel panoları da yükleyebilirsiniz.
