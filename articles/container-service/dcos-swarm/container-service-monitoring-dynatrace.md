---
title: "aaaMonitor Azure DC/OS kümesi - Dynatrace | Microsoft Docs"
description: "Azure kapsayıcı hizmeti DC/OS kümesi Dynatrace ile izleyin. Merhaba Dynatrace OneAgent hello DC/OS panosunu kullanarak dağıtın."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a>Azure kapsayıcı hizmeti DC/OS kümesi Dynatrace SaaS/yönetilen'ile izleme
Bu makalede, nasıl gösteriyoruz toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor tüm hello Azure kapsayıcı hizmeti kümenizdeki düğümlerin Aracısı. Bu yapılandırma için bir hesap ile Dynatrace SaaS/yönetilen gerekir. 

## <a name="dynatrace-saasmanaged"></a>Dynatrace SaaS/yönetilen
Dynatrace bir bulut yerel izleme için yüksek oranda dinamik kapsayıcı ve küme ortamları çözümüdür. Bu sayede toobetter en iyi duruma getirme kapsayıcı dağıtımlarını ve bellek ayırma gerçek zamanlı kullanım verilerini kullanarak. Otomatik olarak uygulama ve altyapı sorunları otomatik taban çizgisi oluşturma, sorunu bağıntı ve temel nedenin algılama sağlayarak yerini tam olarak belirtmekte yeteneğine sahiptir.

Merhaba aşağıdaki gösterir hello Dynatrace UI şekil:

![Dynatrace kullanıcı Arabirimi](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a>Ön koşullar 
[Dağıtma](container-service-deployment.md) ve [bağlanmak](./../container-service-connect.md) tooa küme Azure kapsayıcı hizmeti tarafından yapılandırılır. Merhaba keşfedin [Marathon kullanıcı Arabirimi](container-service-mesos-marathon-ui.md). Çok Git[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset Dynatrace SaaS hesabı.  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a>Marathon ile Dynatrace dağıtımını yapılandırma
Bu adımlar şunları nasıl yapacağınızı tooconfigure ve Dynatrace uygulamaları tooyour küme Marathon ile dağıtın.

1. DC/OS kullanıcı Arabirimi aracılığıyla erişim [http://localhost:80 /](http://localhost:80/). Bir kez hello DC/OS kullanıcı Arabirimi, toohello gidin **Universe** sekmesinde arayın ve sonra **Dynatrace**.

    ![DC/OS Universe Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. toocomplete hello yapılandırması, bir Dynatrace SaaS hesap veya ücretsiz bir deneme hesabı gerekir. Merhaba Dynatrace panoya oturum sonra seçeneğini **dağıtmak Dynatrace**.

    ![PaaS tümleştirme Dynatrace ayarlama](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. Merhaba sayfasında seçin **PaaS tümleştirmesini ayarlama**. 

    ![Dynatrace API belirteci](./media/container-service-monitoring-dynatrace/api-token.png) 

4. Merhaba Dynatrace OneAgent yapılandırma hello DC/OS Universe içinde içine API belirtecinizi girin. 

    ![Merhaba DC/OS Universe Dynatrace OneAgent yapılandırma](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. Merhaba örnekleri kümesi toohello numarası toorun düşündüğünüz düğümlerinin. Bu sayıyı gerçekte ulaşılana kadar daha yüksek bir sayı çalışır, ancak DC/OS ayarı toofind yeni örnekleri denemeye devam edilecek. Tercih ederseniz, bu tooa değer 1000000 gibi de ayarlayabilirsiniz. Bu durumda, yeni bir düğüm toohello küme eklendiğinde Dynatrace otomatik olarak bir aracı toothat yeni düğümü, DC/OS sürekli toodeploy başka örnekler çalışıyor hello fiyatla dağıtır.

    ![Merhaba DC/OS Universe-örnekleri Dynatrace yapılandırma](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a>Sonraki adımlar

Merhaba paketini yükledikten sonra geri toohello Dynatrace Pano gidin. Küme içinde Merhaba kapsayıcılara için hello farklı kullanım ölçümleri gözden geçirebilirsiniz. 
