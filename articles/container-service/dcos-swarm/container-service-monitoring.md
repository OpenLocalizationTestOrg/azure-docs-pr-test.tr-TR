---
title: "İzleyici Azure DC/OS kümesi - Datadog"
description: "Azure kapsayıcı hizmeti kümesi Datadog ile izleyin. Kümenize Datadog aracıları dağıtmak için DC/OS web kullanıcı arabirimini kullanın."
services: container-service
author: sauryadas
manager: timlt
ms.service: container-service
ms.topic: article
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: b895ef906a8c8f3f8cc21267d80f8b59b64837f4
ms.sourcegitcommit: 5d3e99478a5f26e92d1e7f3cec6b0ff5fbd7cedf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a>Azure kapsayıcı hizmeti DC/OS kümesi Datadog ile izleme

Bu makalede, Azure kapsayıcı hizmeti kümesindeki tüm Aracısı düğümleri biz Datadog aracıları dağıtır. Bu yapılandırma için Datadog sahip bir hesap gerekir. 

## <a name="prerequisites"></a>Ön koşullar
Azure Container Service tarafından yapılandırılmış bir kümeyi [dağıtın](container-service-deployment.md) ve [bağlayın](../container-service-connect.md). [Marathon Kullanıcı Arabirimi](container-service-mesos-marathon-ui.md)’ni keşfedin. Git [http://datadoghq.com](http://datadoghq.com) bir Datadog hesabı ayarlamak için. 

## <a name="datadog"></a>Datadog
Datadog, Azure kapsayıcı hizmeti kümesi kapsayıcılara gelen izleme verilerini toplayan izleme bir hizmettir. Datadog Docker tümleştirmesi, kapsayıcılara belirli ölçümleri görebileceğiniz bir Pano vardır. Kapsayıcılardan toplanan ölçümleri CPU, bellek, ağ ve g/ç tarafından düzenlenir. Datadog ölçümleri kapsayıcıları ve görüntüleri halinde ayırır. Kullanıcı arabirimini nasıl için CPU kullanımını göründüğünü örneği aşağıda verilmiştir.

![Datadog kullanıcı Arabirimi](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a>Marathon ile Datadog dağıtımını yapılandırma
Bu adımları yapılandırmak ve Marathon kümenizle Datadog uygulamaları dağıtmak nasıl yapacağınızı gösterir. 

DC/OS kullanıcı Arabirimi aracılığıyla erişim [http://localhost:80 /](http://localhost:80/). DC/OS kullanıcı Arabiriminde "sol alta olan Universe" kez gidin ve "Datadog" için arama yapın ve "Yükle" yi tıklatın.

![Datadog paket DC/OS Universe içinde](./media/container-service-monitoring/datadog1.png)

Şimdi yapılandırmasını tamamlamak için bir Datadog hesap veya ücretsiz bir deneme hesabı gerekir. Sol Datadog Web sitesi görünüm için oturum açtınız ve tümleştirmeler gidin sonra sonra -> [API'leri](https://app.datadoghq.com/account/settings#api). 

![Datadog API anahtarı](./media/container-service-monitoring/datadog2.png)

Sonraki DC/OS Universe içinde Datadog yapılandırma içine API anahtarınızı girin. 

![DC/OS Universe Datadog yapılandırma](./media/container-service-monitoring/datadog3.png) 

Yukarıdaki yapılandırmada örnekleri 10000000 için ayarlanmış olan bunu yeni bir düğüm kümeye Datadog otomatik olarak bu düğüme bir aracı dağıtacağınız eklendiği zaman. Bu geçici bir çözümdür. Tekrar Datadog Web sitesine gidin ve bulmak paketini yükledikten sonra "[panolar](https://app.datadoghq.com/dash/list)." Buradan, özel ve tümleştirme panolar görürsünüz. [Docker Pano](https://app.datadoghq.com/screen/integration/docker) kümenizi izleme için gereksinim duyduğunuz tüm kapsayıcı ölçümleri sahip olur. 

