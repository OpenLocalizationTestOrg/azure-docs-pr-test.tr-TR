---
title: "aaaMonitor Azure DC/OS kümesi - Datadog | Microsoft Docs"
description: "Azure kapsayıcı hizmeti kümesi Datadog ile izleyin. Merhaba DC/OS web kullanıcı Arabirimi toodeploy hello Datadog aracıları tooyour kümesi kullanın."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, DC/OS, Docker Swarm, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a>Azure kapsayıcı hizmeti DC/OS kümesi Datadog ile izleme
Bu makalede biz Datadog aracıları tooall hello Aracısı düğümleri, Azure kapsayıcı hizmeti kümesi dağıtır. Bu yapılandırma için Datadog sahip bir hesap gerekir. 

## <a name="prerequisites"></a>Ön koşullar
Azure Container Service tarafından yapılandırılmış bir kümeyi [dağıtın](container-service-deployment.md) ve [bağlayın](../container-service-connect.md). Merhaba keşfedin [Marathon kullanıcı Arabirimi](container-service-mesos-marathon-ui.md). Çok Git[http://datadoghq.com](http://datadoghq.com) tooset Datadog hesabı. 

## <a name="datadog"></a>Datadog
Datadog, Azure kapsayıcı hizmeti kümesi kapsayıcılara gelen izleme verilerini toplayan izleme bir hizmettir. Datadog Docker tümleştirmesi, kapsayıcılara belirli ölçümleri görebileceğiniz bir Pano vardır. Kapsayıcılardan toplanan ölçümleri CPU, bellek, ağ ve g/ç tarafından düzenlenir. Datadog ölçümleri kapsayıcıları ve görüntüleri halinde ayırır. Hangi hello örneği için CPU kullanımı aşağıdadır UI görülüyor.

![Datadog kullanıcı Arabirimi](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a>Marathon ile Datadog dağıtımını yapılandırma
Bu adımlar şunları nasıl yapacağınızı gösterilecek tooconfigure ve Datadog uygulamaları tooyour küme Marathon ile dağıtın. 

DC/OS kullanıcı Arabirimi aracılığıyla erişim [http://localhost:80 /](http://localhost:80/). Bir kez DC/OS kullanıcı Arabirimi gidin hello toohello "Merhaba üzerinde olan Universe" sol alt ve "Datadog" için arama yapın ve "Yükle" yi tıklatın.

![Datadog paket hello DC/OS Universe içinde](./media/container-service-monitoring/datadog1.png)

Toocomplete hello artık yapılandırma Datadog hesap veya ücretsiz bir deneme hesabı gerekir. Oturum açtınız sonra toohello sol toohello Datadog Web sitesine bakın ve Git tooIntegrations -> sonra [API'leri](https://app.datadoghq.com/account/settings#api). 

![Datadog API anahtarı](./media/container-service-monitoring/datadog2.png)

Sonraki hello Datadog yapılandırma hello DC/OS Universe içinde içine API anahtarınızı girin. 

![Merhaba DC/OS Universe Datadog yapılandırma](./media/container-service-monitoring/datadog3.png) 

Yeni bir düğüm eklendiğinde toohello küme Datadog otomatik olarak bir aracı toothat düğümüne dağıtacak şekilde hello yapılandırma yukarıda örnekleri too10000000 ayarlanır. Bu geçici bir çözümdür. Merhaba paketini yükledikten sonra geri toohello Datadog Web sitesine gidin ve bulmak gerekir "[panolar](https://app.datadoghq.com/dash/list)." Buradan, özel ve tümleştirme panolar görürsünüz. Merhaba [Docker Pano](https://app.datadoghq.com/screen/integration/docker) kümenizi izleme için gereksinim duyduğunuz tüm hello kapsayıcı ölçümleri sahip olur. 

