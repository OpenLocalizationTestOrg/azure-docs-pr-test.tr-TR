---
title: "Azure DC/OS kümesinde aaaCanary sürüm Vamp ile | Microsoft Docs"
description: "Nasıl toouse toocanary yayın Hizmetleri Vamp ve akıllı trafik bir Azure kapsayıcı hizmeti DC/OS kümesinde filtreleme Uygula"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="2f7c7-103">Bir Azure kapsayıcı hizmeti DC/OS kümesinde yalancı yayın mikro Vamp ile</span><span class="sxs-lookup"><span data-stu-id="2f7c7-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="2f7c7-104">Bu kılavuzda, biz Vamp Azure kapsayıcı hizmeti DC/OS kümesi ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="2f7c7-105">Biz yalancı hello Vamp demo hizmeti "sava" yayın ve akıllı trafik filtreleme uygulayarak bir uyumsuzluk hello hizmetinin Firefox ile çözün.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-105">We canary release hello Vamp demo service "sava", and then resolve an incompatibility of hello service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="2f7c7-106">Bu kılavuzda Vamp bir DC/OS kümesinde çalışır, ancak ayrıca Vamp Kubernetes ile Merhaba orchestrator kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as hello orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="2f7c7-107">Yalancı serbest bırakır ve Vamp hakkında</span><span class="sxs-lookup"><span data-stu-id="2f7c7-107">About canary releases and Vamp</span></span>


<span data-ttu-id="2f7c7-108">[Yalancı serbest](https://martinfowler.com/bliki/CanaryRelease.html) olan Netflix, Facebook ve Spotify gibi yenilikçi kuruluşlar tarafından benimsenen akıllı Dağıtım stratejisi.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="2f7c7-109">Sorunları azaltır, ağ güvenliği tanıtır ve yenilik artırır bulunduğundan, mantıklı bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="2f7c7-110">Bu nedenle neden tüm şirketlerin kullanmadığınız?</span><span class="sxs-lookup"><span data-stu-id="2f7c7-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="2f7c7-111">CI/CD ardışık düzen tooinclude yalancı stratejileri genişletme karmaşıklık ekler ve kapsamlı bir devops bilgi ve deneyimlerine gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-111">Extending a CI/CD pipeline tooinclude canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="2f7c7-112">Bile çalışmaya başlamadan önce yeterli tooblock küçük şirket ve kuruluş aynı şekilde olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-112">That’s enough tooblock smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="2f7c7-113">[Vamp](http://vamp.io/) bu geçiş tasarlanmış açık kaynak sistemi tooease olduğu ve yalancı serbest özellikleri tercih edilen tooyour kapsayıcı Zamanlayıcı duruma getirin.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-113">[Vamp](http://vamp.io/) is an open-source system designed tooease this transition and bring canary releasing features tooyour preferred container scheduler.</span></span> <span data-ttu-id="2f7c7-114">Yüzde tabanlı sürülmeleri vamp'ın yalancı işlevselliği gider.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="2f7c7-115">Trafik filtre ve çok çeşitli koşullar, örneğin tootarget belirli kullanıcılar, IP aralıkları veya cihazlar üzerinde bölebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-115">Traffic can be filtered and split on a wide range of conditions, for example tootarget specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="2f7c7-116">Vamp izler ve performans ölçümleri, gerçek verilerine dayalı Otomasyon izin vermeyi analiz eder.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="2f7c7-117">Otomatik geri alma işlemi hatalarla ayarlayın veya bireysel hizmet çeşitleri yük veya gecikme göre ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="2f7c7-118">Azure kapsayıcı hizmeti DC/OS ile ayarlama</span><span class="sxs-lookup"><span data-stu-id="2f7c7-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="2f7c7-119">[DC/OS kümesi dağıtma](container-service-deployment.md) bir ana ve varsayılan boyutunun iki aracı ile.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="2f7c7-120">[SSH tüneli oluşturma](../container-service-connect.md) tooconnect toohello DC/OS kümesi.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-120">[Create an SSH tunnel](../container-service-connect.md) tooconnect toohello DC/OS cluster.</span></span> <span data-ttu-id="2f7c7-121">Bu makale, toohello küme yerel bağlantı noktası 80 üzerinde tünel varsayar.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-121">This article assumes that you tunnel toohello cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="2f7c7-122">Vamp ayarlayın</span><span class="sxs-lookup"><span data-stu-id="2f7c7-122">Set up Vamp</span></span>

<span data-ttu-id="2f7c7-123">Çalışan DC/OS kümesine sahip olduğunuza göre DC/OS kullanıcı Arabirimi (http://localhost:80) hello Vamp yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-123">Now that you have a running DC/OS cluster, you can install Vamp from hello DC/OS UI (http://localhost:80).</span></span> 

![DC/OS Kullanıcı Arabirimi](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="2f7c7-125">Yükleme, iki aşamada yapılır:</span><span class="sxs-lookup"><span data-stu-id="2f7c7-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="2f7c7-126">**Elasticsearch dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="2f7c7-127">Ardından **Vamp dağıtmak** hello Vamp DC/OS universe paketi yükleyerek.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-127">Then **deploy Vamp** by installing hello Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="2f7c7-128">Elasticsearch dağıtma</span><span class="sxs-lookup"><span data-stu-id="2f7c7-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="2f7c7-129">Vamp Elasticsearch ölçümleri toplama ve toplama için gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="2f7c7-130">Merhaba kullanabilirsiniz [magneticio Docker görüntüleri](https://hub.docker.com/r/magneticio/elastic/) toodeploy uyumlu Vamp Elasticsearch yığını.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-130">You can use hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="2f7c7-131">Hello DC/OS kullanıcı Arabirimi, çok Git**Hizmetleri** tıklatıp **hizmeti Dağıt**.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-131">In hello DC/OS UI, go too**Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="2f7c7-132">Seçin **JSON modu** hello gelen **yeni hizmeti Dağıt** açılır.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-132">Select **JSON mode** from hello **Deploy New Service** pop-up.</span></span>

  ![JSON modu seçin](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="2f7c7-134">JSON aşağıdaki hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-134">Paste in hello following JSON.</span></span> <span data-ttu-id="2f7c7-135">Bu yapılandırma, 1 GB RAM ve temel sistem durumu denetimi hello Elasticsearch bağlantı noktası ile Merhaba kapsayıcı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-135">This configuration runs hello container with 1 GB of RAM and a basic health check on hello Elasticsearch port.</span></span>
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. <span data-ttu-id="2f7c7-136">Tıklatın **dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-136">Click **Deploy**.</span></span>

  <span data-ttu-id="2f7c7-137">DC/OS hello Elasticsearch kapsayıcı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-137">DC/OS deploys hello Elasticsearch container.</span></span> <span data-ttu-id="2f7c7-138">Merhaba üzerinde ilerleme durumunu izleyebilirsiniz **Hizmetleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-138">You can track progress on hello **Services** page.</span></span>  

  ![e dağıtabilir? Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="2f7c7-140">Vamp dağıtma</span><span class="sxs-lookup"><span data-stu-id="2f7c7-140">Deploy Vamp</span></span>

<span data-ttu-id="2f7c7-141">Olarak Elasticsearch raporları bir kez **çalıştıran**, hello Vamp DC/OS Universe paket ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-141">Once Elasticsearch reports as **Running**, you can add hello Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="2f7c7-142">Çok Git**Universe** arayın ve **vamp**.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-142">Go too**Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="2f7c7-143">![DC/OS universe üzerinde vamp](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="2f7c7-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="2f7c7-144">Tıklatın **yükleme** sonraki toohello vamp paketi ve seçin **gelişmiş yükleme**.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-144">Click **install** next toohello vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="2f7c7-145">Aşağı kaydırın ve elasticsearch url aşağıdaki hello girin: `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-145">Scroll down and enter hello following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Elasticsearch URL'sini girin](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="2f7c7-147">Tıklatın **gözden geçirin ve yükleyin**, ardından **yükleme** toostart hello dağıtım.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-147">Click **Review and Install**, then click **Install** toostart hello deployment.</span></span>  

  <span data-ttu-id="2f7c7-148">DC/OS gerekli tüm Vamp bileşenlerini dağıtır.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="2f7c7-149">Merhaba üzerinde ilerleme durumunu izleyebilirsiniz **Hizmetleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-149">You can track progress on hello **Services** page.</span></span>
  
  ![Vamp universe paketi olarak dağıtma](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="2f7c7-151">Dağıtım tamamlandıktan sonra hello Vamp UI erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2f7c7-151">Once deployment has completed, you can access hello Vamp UI:</span></span>

  ![DC/OS vamp hizmeti](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![UI vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="2f7c7-154">İlk hizmetiniz dağıtma</span><span class="sxs-lookup"><span data-stu-id="2f7c7-154">Deploy your first service</span></span>

<span data-ttu-id="2f7c7-155">Bu Vamp çalışır durumda artık şeması hizmetinden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="2f7c7-156">En basit biçimiyle içinde bir [Vamp şeması](http://vamp.io/documentation/using-vamp/blueprints/) hello uç noktaları (ağ geçidi), kümeler ve Hizmetleri toodeploy açıklar.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes hello endpoints (gateways), clusters, and services toodeploy.</span></span> <span data-ttu-id="2f7c7-157">Kullanan kümeler toogroup farklı türevleri aynı hizmet mantıksal gruplar halinde yalancı serbest bırakma veya bir hello vamp / B testi.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-157">Vamp uses clusters toogroup different variants of hello same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="2f7c7-158">Bu senaryo adlı örnek bir tek yapılı uygulama kullanır [ **sava**](https://github.com/magneticio/sava), sürüm 1.0 olduğu.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="2f7c7-159">Merhaba monolith Docker Hub magneticio/sava:1.0.0 altında olan bir Docker kapsayıcısı paketlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-159">hello monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="2f7c7-160">Merhaba uygulama normalde bağlantı noktası 8080 üzerinde çalışır, ancak altında bağlantı noktası 9050 bu durumda tooexpose istiyor.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-160">hello app normally runs on port 8080, but you want tooexpose it under port 9050 in this case.</span></span> <span data-ttu-id="2f7c7-161">Basit şeması kullanarak Vamp aracılığıyla Hello uygulamasını dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-161">Deploy hello app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="2f7c7-162">Çok Git**dağıtımları**.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-162">Go too**Deployments**.</span></span>

2. <span data-ttu-id="2f7c7-163">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-163">Click **Add**.</span></span>

3. <span data-ttu-id="2f7c7-164">Aşağıdaki hello yapıştırma seçeneğiyle şeması YAML.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-164">Paste in hello following blueprint YAML.</span></span> <span data-ttu-id="2f7c7-165">Bu şeması sizi bir sonraki adımda değiştirmek yalnızca bir hizmet değişken ile tek bir küme içerir:</span><span class="sxs-lookup"><span data-stu-id="2f7c7-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="2f7c7-166">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-166">Click **Save**.</span></span> <span data-ttu-id="2f7c7-167">Vamp hello dağıtım başlatır.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-167">Vamp initiates hello deployment.</span></span>

<span data-ttu-id="2f7c7-168">Merhaba dağıtım üzerinde hello listelenen **dağıtımları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-168">hello deployment is listed on hello **Deployments** page.</span></span> <span data-ttu-id="2f7c7-169">Merhaba dağıtım toomonitor durumunu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-169">Click hello deployment toomonitor its status.</span></span>

![UI Sava dağıtma - vamp](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Kullanıcı arabiriminde Vamp Sava hizmeti](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="2f7c7-172">İki ağ geçidi oluşturulur, hangi hello üzerinde listelenen **ağ geçitleri** sayfa:</span><span class="sxs-lookup"><span data-stu-id="2f7c7-172">Two gateways are created, which are listed on hello **Gateways** page:</span></span>

* <span data-ttu-id="2f7c7-173">hizmetini (bağlantı noktası 9050) çalıştıran bir kararlı endpoint tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="2f7c7-173">a stable endpoint tooaccess hello running service (port 9050)</span></span> 
* <span data-ttu-id="2f7c7-174">bir Vamp yönetilen iç ağ geçidi (daha sonra bu ağ geçidi hakkında daha fazla).</span><span class="sxs-lookup"><span data-stu-id="2f7c7-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![UI - sava ağ geçitleri vamp](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="2f7c7-176">Hello sava hizmeti şimdi dağıtıldığını, ancak hello Azure yük dengeleyici tooforward trafiği tooit henüz bilmiyor, dışarıdan erişemezler.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-176">hello sava service has now deployed, but you can’t access it externally because hello Azure Load Balancer doesn’t know tooforward traffic tooit yet.</span></span> <span data-ttu-id="2f7c7-177">tooaccess hello hizmeti, güncelleştirme hello Azure ağ yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-177">tooaccess hello service, update hello Azure networking configuration.</span></span>


## <a name="update-hello-azure-network-configuration"></a><span data-ttu-id="2f7c7-178">Hello Azure ağ yapılandırmasını güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="2f7c7-178">Update hello Azure network configuration</span></span>

<span data-ttu-id="2f7c7-179">Dağıtılan hello sava düğümlerde hizmetini kararlı bir uç nokta bağlantı noktası 9050 gösterme hello DC/OS Aracısı, vamp.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-179">Vamp deployed hello sava service on hello DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="2f7c7-180">Dış hello DC/OS kümesi tooaccess hello hizmetinden değişiklikleri toohello Azure ağ yapılandırması, küme dağıtımınızda aşağıdaki hello olun:</span><span class="sxs-lookup"><span data-stu-id="2f7c7-180">tooaccess hello service from outside hello DC/OS cluster, make hello following changes toohello Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="2f7c7-181">**Hello Azure yük dengeleyici yapılandırma** hello aracılar için (Merhaba adlı kaynak **dcos-aracı-lb-xxxx**) durum araştırması ve bağlantı noktası 9050 toohello sava örneklerinde kuralı tooforward trafiği ile.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-181">**Configure hello Azure Load Balancer** for hello agents (hello resource named **dcos-agent-lb-xxxx**) with a health probe and a rule tooforward traffic on port 9050 toohello sava instances.</span></span> 

2. <span data-ttu-id="2f7c7-182">**Güncelleştirme hello ağ güvenlik grubu** hello ortak aracılar için (Merhaba adlı kaynak **XXXX-aracı-genel-nsg-XXXX**) bağlantı noktası 9050 tooallow trafiğine.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-182">**Update hello network security group** for hello public agents (hello resource named **XXXX-agent-public-nsg-XXXX**) tooallow traffic on port 9050.</span></span>

<span data-ttu-id="2f7c7-183">Azure portal, bkz: kullanarak bu görevleri için ayrıntılı adımlar toocomplete hello [etkinleştirmek genel erişim tooan Azure kapsayıcı hizmeti uygulama](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="2f7c7-183">For detailed steps toocomplete these tasks using hello Azure portal, see [Enable public access tooan Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="2f7c7-184">Bağlantı noktasını 9050 tüm bağlantı noktası ayarlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="2f7c7-185">Her şeyi oluşturulduktan sonra toohello Git **genel bakış** dikey penceresinde hello DC/OS Aracısı Yük Dengeleyici (Merhaba adlı kaynak **dcos-aracı-lb-xxxx**).</span><span class="sxs-lookup"><span data-stu-id="2f7c7-185">Once everything has been created, go toohello **Overview** blade of hello DC/OS agent load balancer (hello resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="2f7c7-186">Hello bulur **genel IP adresi**ve hello adresi tooaccess sava 9050 numaralı bağlantı noktasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-186">Find hello **Public IP address**, and use hello address tooaccess sava at port 9050.</span></span>

![Azure portal - get genel IP adresi](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![Sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="2f7c7-189">Yalancı yayın çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2f7c7-189">Run a canary release</span></span>

<span data-ttu-id="2f7c7-190">Üretime toocanary yayın istediğiniz bir uygulamanın yeni sürümü bu olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-190">Suppose you have a new version of this application that you want toocanary release into production.</span></span> <span data-ttu-id="2f7c7-191">Magneticio/sava:1.1.0 kapsayıcılı olması ve hazır toogo şunlardır.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-191">You have it containerized as magneticio/sava:1.1.0 and are ready toogo.</span></span> <span data-ttu-id="2f7c7-192">Vamp dağıtımı çalıştıran yeni hizmetleri toohello kolayca eklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-192">Vamp lets you easily add new services toohello running deployment.</span></span> <span data-ttu-id="2f7c7-193">"Birleştirilmiş" hizmetlerin hello varolan Hizmetleri hello kümedeki yanında dağıtılan ve Ağırlık % 0 olarak atanmış.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-193">These "merged" services are deployed alongside hello existing services in hello cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="2f7c7-194">Merhaba trafik dağılımı ayarlamak kadar hiçbir trafik yeni birleştirilmiş yönlendirilmiş tooa hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-194">No traffic is routed tooa newly merged service until you adjust hello traffic distribution.</span></span> <span data-ttu-id="2f7c7-195">Merhaba ağırlık kaydırıcı hello Vamp UI içinde artımlı ayarlamalar (yalancı sürüm) ya da anlık bir geri alma için izin verme hello dağıtım üzerinde tam denetim verir.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-195">hello weight slider in hello Vamp UI gives you complete control over hello distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="2f7c7-196">Yeni bir hizmet değişken birleştirme</span><span class="sxs-lookup"><span data-stu-id="2f7c7-196">Merge a new service variant</span></span>

<span data-ttu-id="2f7c7-197">toomerge hello yeni sava 1.1 hizmetiyle dağıtımı çalıştıran hello:</span><span class="sxs-lookup"><span data-stu-id="2f7c7-197">toomerge hello new sava 1.1 service with hello running deployment:</span></span>

1. <span data-ttu-id="2f7c7-198">Hello Vamp UI, tıklatın **planlar**.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-198">In hello Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="2f7c7-199">Tıklatın **Ekle** ve Yapıştır aşağıdaki hello'şeması YAML: yeni bir hizmet değişken (sava: 1.1.0) toodeploy hello var olan küme (sava_cluster) içinde bu şeması açıklar.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-199">Click **Add** and paste in hello following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) toodeploy within hello existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. <span data-ttu-id="2f7c7-200">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-200">Click **Save**.</span></span> <span data-ttu-id="2f7c7-201">Merhaba şeması depolanır ve üzerinde hello listelenen **planlar** sayfası.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-201">hello blueprint is stored and listed on hello **Blueprints** page.</span></span>

4. <span data-ttu-id="2f7c7-202">Açık hello Eylem menüsünde tıklatın ve hello sava: 1.1 şeması **birleştirilecek**.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-202">Open hello action menu on hello sava:1.1 blueprint and click **Merge to**.</span></span>

  ![UI - planlar vamp](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="2f7c7-204">Select hello **sava** dağıtım ve tıklatın **birleştirme**.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-204">Select hello **sava** deployment and click **Merge**.</span></span>

  ![UI vamp - şeması toodeployment birleştirme](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="2f7c7-206">Vamp dağıtır hello şeması sava: hello 1.0.0 yanında açıklanan hello yeni sava: 1.1.0 hizmeti değişken **sava_cluster** hello dağıtımı çalıştıran biri.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-206">Vamp deploys hello new sava:1.1.0 service variant described in hello blueprint alongside sava:1.0.0 in hello **sava_cluster** of hello running deployment.</span></span> 

![UI - güncelleştirilmiş sava dağıtım vamp](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="2f7c7-208">Merhaba **sava_cluster/sava/webport** ağ geçidi (Merhaba küme uç noktası) da güncelleştirilmiş, dağıtılan sava: 1.1.0 rota toohello yeni ekleme.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-208">hello **sava/sava_cluster/webport** gateway (hello cluster endpoint) is also updated, adding a route toohello newly deployed sava:1.1.0.</span></span> <span data-ttu-id="2f7c7-209">Bu noktada, hiçbir trafik burada yönlendirilen (Merhaba **ağırlık** too0% ayarlanır).</span><span class="sxs-lookup"><span data-stu-id="2f7c7-209">At this point, no traffic is routed here (hello **WEIGHT** is set too0%).</span></span>

![UI - küme ağ geçidi vamp](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="2f7c7-211">Yalancı sürüm</span><span class="sxs-lookup"><span data-stu-id="2f7c7-211">Canary release</span></span>

<span data-ttu-id="2f7c7-212">Her iki sava sürümleriyle dağıtılan hello aynı küme, hello taşıyarak aralarındaki trafik hello dağıtımını Ayarla **ağırlık** kaydırıcı.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-212">With both versions of sava deployed in hello same cluster, adjust hello distribution of traffic between them by moving hello **WEIGHT** slider.</span></span>

1. <span data-ttu-id="2f7c7-213">Tıklatın ![Vamp UI - Düzenle](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) sonraki çok**ağırlık**.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT**.</span></span>

2. <span data-ttu-id="2f7c7-214">Merhaba ağırlık dağıtım too50%/50% ayarlayın ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-214">Set hello weight distribution too50%/50% and click **Save**.</span></span>

  ![UI - ağ geçidi ağırlık kaydırıcı vamp](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="2f7c7-216">Tooyour tarayıcı geri dönün ve birkaç kere hello sava sayfayı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-216">Go back tooyour browser and refresh hello sava page a few more times.</span></span> <span data-ttu-id="2f7c7-217">Merhaba sava uygulamayı şimdi sava: 1.0 sayfa sava: 1.1 sayfa arasında geçiş yapar.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-217">hello sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![değişen sava1.0 ve sava1.1 Hizmetleri](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="2f7c7-219">Bu değişim hello sayfasının en iyi hello "Incognito" veya "Anonim" modu tarayıcınızın hello statik varlıklarını önbelleğe alma nedeniyle çalışır.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-219">This alternation of hello page works best with hello "Incognito" or “Anonymous” mode of your browser because of hello caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="2f7c7-220">Trafik filtre</span><span class="sxs-lookup"><span data-stu-id="2f7c7-220">Filter traffic</span></span>

<span data-ttu-id="2f7c7-221">Dağıtımdan sonra bir uyumsuzluk sava: 1.1.0 nedenleri Firefox tarayıcılarda sorunları görüntülemek içinde bulunan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="2f7c7-222">Vamp toofilter gelen trafiği ayarlayın ve kararlı sava: 1.0.0 bilinen toohello tüm Firefox kullanıcıları geri doğrudan.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-222">You can set Vamp toofilter incoming traffic and direct all Firefox users back toohello known stable sava:1.0.0.</span></span> <span data-ttu-id="2f7c7-223">Başka bir herkes tooenjoy hello hello yararları devam ederken çözümler Firefox kullanıcılar için kesintiyi hello instantly Bu filtre sava: 1.1.0 geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-223">This filter instantly resolves hello disruption for Firefox users, while everybody else continues tooenjoy hello benefits of hello improved sava:1.1.0.</span></span>

<span data-ttu-id="2f7c7-224">Kullanır vamp **koşullar** toofilter trafiği bir ağ geçidi yollar arasında.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-224">Vamp uses **conditions** toofilter traffic between routes in a gateway.</span></span> <span data-ttu-id="2f7c7-225">Trafik ilk filtre ve according toohello uygulanan koşullar tooeach rota yönlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-225">Traffic is first filtered and directed according toohello conditions applied tooeach route.</span></span> <span data-ttu-id="2f7c7-226">Tüm kalan trafik toohello ağ geçidi ağırlığı ayarı göre dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-226">All remaining traffic is distributed according toohello gateway weight setting.</span></span>

<span data-ttu-id="2f7c7-227">Bir koşul toofilter tüm Firefox kullanıcıları oluşturun ve bunları toohello eski sava: 1.0.0 doğrudan:</span><span class="sxs-lookup"><span data-stu-id="2f7c7-227">You can create a condition toofilter all Firefox users and direct them toohello old sava:1.0.0:</span></span>

1. <span data-ttu-id="2f7c7-228">Merhaba sava/sava_cluster/webport üzerinde **ağ geçitleri** sayfasında, ![Vamp UI - Düzenle](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd bir **KOŞULU** toohello rota sava/sava_cluster/sava:1.0.0/webport.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-228">On hello sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd a **CONDITION** toohello route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="2f7c7-229">Merhaba koşulu girin **kullanıcı aracısı Firefox ==** tıklatıp ![Vamp UI - Kaydet](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="2f7c7-229">Enter hello condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="2f7c7-230">Vamp %0 varsayılan gücü ile Merhaba koşulu ekler.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-230">Vamp adds hello condition with a default strength of 0%.</span></span> <span data-ttu-id="2f7c7-231">trafiği filtreleyerek toostart, tooadjust hello koşul gücü gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-231">toostart filtering traffic, you need tooadjust hello condition strength.</span></span>

3. <span data-ttu-id="2f7c7-232">Tıklatın ![Vamp UI - Düzenle](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **gücü** uygulanan toohello koşulu.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **STRENGTH** applied toohello condition.</span></span>
 
4. <span data-ttu-id="2f7c7-233">Set hello **gücü** too100% tıklatıp ![Vamp UI - Kaydet](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-233">Set hello **STRENGTH** too100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span></span>

  <span data-ttu-id="2f7c7-234">Vamp şimdi hello koşul (tüm Firefox kullanıcılar) toosava:1.0.0 eşleşen tüm trafik gönderir.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-234">Vamp now sends all traffic matching hello condition (all Firefox users) toosava:1.0.0.</span></span>

  ![UI vamp - koşul toogateway Uygula](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="2f7c7-236">Son olarak, tüm kalan trafik (tüm Firefox olmayan kullanıcılar) toohello yeni sava: 1.1.0 hello ağ geçidi ağırlık toosend ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-236">Finally, adjust hello gateway weight toosend all remaining traffic (all non-Firefox users) toohello new sava:1.1.0.</span></span> <span data-ttu-id="2f7c7-237">Tıklatın ![Vamp UI - Düzenle](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) sonraki çok**ağırlık** ve yönlendirilmiş toohello rota sava/sava_cluster/sava:1.1.0/webport % 100 olacak şekilde hello ağırlık dağıtımı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT** and set hello weight distribution so 100% is directed toohello route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="2f7c7-238">Merhaba koşul tarafından filtrelenmiş olmayan tüm trafiği yönlendirilmiş toohello yeni sava: 1.1.0 sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-238">All traffic not filtered by hello condition is now directed toohello new sava:1.1.0.</span></span>

6. <span data-ttu-id="2f7c7-239">Eylem toosee hello filtre iki farklı tarayıcılar (bir Firefox ve başka bir tarayıcı) açın ve hello sava hizmet hem de erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-239">toosee hello filter in action, open two different browsers (one Firefox and one other browser) and access hello sava service from both.</span></span> <span data-ttu-id="2f7c7-240">Diğer tüm tarayıcılar yönlendirilmiş toosava:1.1.0 çalışırken tüm Firefox istekleri toosava:1.0.0, gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-240">All Firefox requests are sent toosava:1.0.0, while all other browsers are directed toosava:1.1.0.</span></span>

  ![UI - filtre trafiği vamp](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="2f7c7-242">Özetle</span><span class="sxs-lookup"><span data-stu-id="2f7c7-242">Summing up</span></span>

<span data-ttu-id="2f7c7-243">Bu makalede Hızlı Giriş tooVamp bir DC/OS kümesinde oluştu.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-243">This article was a quick introduction tooVamp on a DC/OS cluster.</span></span> <span data-ttu-id="2f7c7-244">Yeni başlayanlar Vamp var ve, Azure kapsayıcı hizmeti DC/OS üzerinde çalışan küme, hizmet Vamp şeması ile dağıtılmış ve kullanıma sunulan hello uç noktasında (ağ geçidi) erişilen.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at hello exposed endpoint (gateway).</span></span>

<span data-ttu-id="2f7c7-245">Biz de güçlü özelliklerinden bazıları Vamp üzerinde işlemdeki: çalışan dağıtım ve artımlı olarak giriş ve ardından trafik tooresolve bilinen bir uyumsuzluk filtreleme bir yeni hizmet değişken toohello birleştirme.</span><span class="sxs-lookup"><span data-stu-id="2f7c7-245">We also touched on some powerful features of Vamp:  merging a new service variant toohello running deployment and introducing it incrementally, then filtering traffic tooresolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2f7c7-246">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2f7c7-246">Next steps</span></span>

* <span data-ttu-id="2f7c7-247">Merhaba aracılığıyla Vamp eylemleri yönetme hakkında bilgi edinin [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="2f7c7-247">Learn about managing Vamp actions through hello [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="2f7c7-248">Node.js içinde Vamp Otomasyon betikleri oluşturmak ve bunları olarak çalıştırma [Vamp iş akışları](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="2f7c7-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="2f7c7-249">Bkz: ek [VAMP öğreticileri](http://vamp.io/documentation/tutorials/overview/).</span><span class="sxs-lookup"><span data-stu-id="2f7c7-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

