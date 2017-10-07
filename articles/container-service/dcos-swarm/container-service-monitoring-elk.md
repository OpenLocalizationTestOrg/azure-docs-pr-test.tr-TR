---
title: "bir Azure DC/OS kümesi - ELK yığın aaaMonitor | Microsoft Docs"
description: "Azure kapsayıcı hizmeti kümesi ELK (Elasticsearch, Logstash ve Kibana) ile DC/OS kümesinde izleyin."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, DC/OS, Azure, izleme, elk"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a>Azure kapsayıcı hizmeti kümesi ELK ile izleme
Bu makalede, Azure kapsayıcı hizmeti DC/OS kümesinde toodeploy hello ELK (Elasticsearch, Logstash, Kibana) nasıl yığın göstermektedir. 

## <a name="prerequisites"></a>Ön koşullar
[Dağıtma](container-service-deployment.md) ve [bağlanmak](../container-service-connect.md) Azure kapsayıcı hizmeti tarafından yapılandırılan bir DC/OS kümesi. Merhaba DC/OS Pano ve Marathon Hizmetleri keşfedin [burada](container-service-mesos-marathon-ui.md). Merhaba yüklemeye [Marathon yük dengeleyici](container-service-load-balancing.md).


## <a name="elk-elasticsearch-logstash-kibana"></a>ELK (Elasticsearch, Logstash, Kibana)
ELK yığın Elasticsearch, Logstash, bir bileşimidir ve sağlayan bir son tooend yığın Kibana kullanılan toomonitor olması ve kümenizdeki günlüklerini analiz edin.

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a>DC/OS kümesinde Hello ELK yığını yapılandırma
DC/OS kullanıcı Arabirimi aracılığıyla erişim [http://localhost:80 /](http://localhost:80/) kez DC/OS kullanıcı Arabirimi gidin çok hello içinde**Universe**. Arama ve Elasticsearch, Logstash ve Kibana hello DC/OS Universe ve bu belirli sırayla yükleyin. Toohello giderseniz yapılandırma hakkında daha fazla bilgiyi **gelişmiş yükleme** bağlantı.

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

Bir kez ELK kapsayıcıları ve çalışır durumdadır Merhaba, Marathon-LB erişilen tooenable Kibana toobe gerekir. Çok gidin **Hizmetleri** > **kibana**, tıklatıp **Düzenle** aşağıda gösterildiği gibi.

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


Çok geçiş**JSON modu** ve toohello etiketleri bölümüne aşağı kaydırın.
Tooadd gereken bir `"HAPROXY_GROUP": "external"` girişi aşağıda gösterildiği gibi aşağıdaki.
Tıkladığınızda **dağıtmak değişiklikleri**, kapsayıcı yeniden başlatılır.

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


Tooverify istiyorsanız, o Kibana hello HAPROXY panosunda hizmet olarak kayıtlı, HAPROXY 9090 bağlantı noktası üzerinde çalışırken hello Aracısı kümede tooopen bağlantı noktası 9090 gerekir.
Varsayılan olarak, biz bağlantı noktası 80, 8080 açın ve DC/OS Aracısı küme içinde 443 hello.
Yönergeler tooopen bir bağlantı noktası ve genel değerlendirme sağlamak sağlanan [burada](container-service-enable-public-access.md).

tooaccess HAPROXY Pano, açık hello Marathon-LB yönetici arabirimin hello: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.
Toohello URL gidin sonra hello HAPROXY Pano aşağıda gösterildiği gibi görmeniz gerekir ve bir hizmet girişi için Kibana görmeniz gerekir.

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


bağlantı noktası 5601 dağıtılır, tooaccess hello Kibana Pano tooopen bağlantı noktası 5601 gerekir. Yönergeleri izleyerek [burada](container-service-enable-public-access.md). Merhaba Kibana Panosu'nda açın: `http://localhost:5601`.

## <a name="next-steps"></a>Sonraki adımlar

* Sistem ve uygulama günlüğü için bkz: iletme ve Kurulum, [DC/OS ELK ile günlük yönetiminde](https://docs.mesosphere.com/1.8/administration/logging/elk/).

* toofilter günlüklerine bakın [ELK filtreleme günlükleriyle](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/). 

 

