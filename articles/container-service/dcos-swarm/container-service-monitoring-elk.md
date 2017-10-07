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
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="e1ab0-104">Azure kapsayıcı hizmeti kümesi ELK ile izleme</span><span class="sxs-lookup"><span data-stu-id="e1ab0-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="e1ab0-105">Bu makalede, Azure kapsayıcı hizmeti DC/OS kümesinde toodeploy hello ELK (Elasticsearch, Logstash, Kibana) nasıl yığın göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-105">In this article, we demonstrate how toodeploy hello ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e1ab0-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e1ab0-106">Prerequisites</span></span>
<span data-ttu-id="e1ab0-107">[Dağıtma](container-service-deployment.md) ve [bağlanmak](../container-service-connect.md) Azure kapsayıcı hizmeti tarafından yapılandırılan bir DC/OS kümesi.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="e1ab0-108">Merhaba DC/OS Pano ve Marathon Hizmetleri keşfedin [burada](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="e1ab0-108">Explore hello DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="e1ab0-109">Merhaba yüklemeye [Marathon yük dengeleyici](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="e1ab0-109">Also install hello [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="e1ab0-110">ELK (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="e1ab0-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="e1ab0-111">ELK yığın Elasticsearch, Logstash, bir bileşimidir ve sağlayan bir son tooend yığın Kibana kullanılan toomonitor olması ve kümenizdeki günlüklerini analiz edin.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end tooend stack that can be used toomonitor and analyze logs in your cluster.</span></span>

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="e1ab0-112">DC/OS kümesinde Hello ELK yığını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e1ab0-112">Configure hello ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="e1ab0-113">DC/OS kullanıcı Arabirimi aracılığıyla erişim [http://localhost:80 /](http://localhost:80/) kez DC/OS kullanıcı Arabirimi gidin çok hello içinde**Universe**.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate too**Universe**.</span></span> <span data-ttu-id="e1ab0-114">Arama ve Elasticsearch, Logstash ve Kibana hello DC/OS Universe ve bu belirli sırayla yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-114">Search and install Elasticsearch, Logstash, and Kibana from hello DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="e1ab0-115">Toohello giderseniz yapılandırma hakkında daha fazla bilgiyi **gelişmiş yükleme** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-115">You can learn more about configuration if you go toohello **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="e1ab0-119">Bir kez ELK kapsayıcıları ve çalışır durumdadır Merhaba, Marathon-LB erişilen tooenable Kibana toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-119">Once hello ELK containers and are up and running, you need tooenable Kibana toobe accessed through Marathon-LB.</span></span> <span data-ttu-id="e1ab0-120">Çok gidin **Hizmetleri** > **kibana**, tıklatıp **Düzenle** aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-120">Navigate too **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="e1ab0-122">Çok geçiş**JSON modu** ve toohello etiketleri bölümüne aşağı kaydırın.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-122">Toggle too**JSON mode** and scroll down toohello labels section.</span></span>
<span data-ttu-id="e1ab0-123">Tooadd gereken bir `"HAPROXY_GROUP": "external"` girişi aşağıda gösterildiği gibi aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-123">You need tooadd a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="e1ab0-124">Tıkladığınızda **dağıtmak değişiklikleri**, kapsayıcı yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="e1ab0-126">Tooverify istiyorsanız, o Kibana hello HAPROXY panosunda hizmet olarak kayıtlı, HAPROXY 9090 bağlantı noktası üzerinde çalışırken hello Aracısı kümede tooopen bağlantı noktası 9090 gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-126">If you want tooverify that Kibana is registered as a service in hello HAPROXY dashboard, you need tooopen port 9090 on hello agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="e1ab0-127">Varsayılan olarak, biz bağlantı noktası 80, 8080 açın ve DC/OS Aracısı küme içinde 443 hello.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-127">By default, we open ports 80, 8080, and 443 in hello DC/OS agent cluster.</span></span>
<span data-ttu-id="e1ab0-128">Yönergeler tooopen bir bağlantı noktası ve genel değerlendirme sağlamak sağlanan [burada](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="e1ab0-128">Instructions tooopen a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="e1ab0-129">tooaccess HAPROXY Pano, açık hello Marathon-LB yönetici arabirimin hello: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-129">tooaccess hello HAPROXY dashboard, open hello Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="e1ab0-130">Toohello URL gidin sonra hello HAPROXY Pano aşağıda gösterildiği gibi görmeniz gerekir ve bir hizmet girişi için Kibana görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-130">Once you navigate toohello URL, you should see hello HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="e1ab0-132">bağlantı noktası 5601 dağıtılır, tooaccess hello Kibana Pano tooopen bağlantı noktası 5601 gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-132">tooaccess hello Kibana dashboard, which is deployed on port 5601, you need tooopen port 5601.</span></span> <span data-ttu-id="e1ab0-133">Yönergeleri izleyerek [burada](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="e1ab0-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="e1ab0-134">Merhaba Kibana Panosu'nda açın: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="e1ab0-134">Then open hello Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1ab0-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1ab0-135">Next steps</span></span>

* <span data-ttu-id="e1ab0-136">Sistem ve uygulama günlüğü için bkz: iletme ve Kurulum, [DC/OS ELK ile günlük yönetiminde](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span><span class="sxs-lookup"><span data-stu-id="e1ab0-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="e1ab0-137">toofilter günlüklerine bakın [ELK filtreleme günlükleriyle](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span><span class="sxs-lookup"><span data-stu-id="e1ab0-137">toofilter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

