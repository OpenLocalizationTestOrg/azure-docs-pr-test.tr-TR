---
title: "Azure DC/OS kümesinde yalancı sürüm Vamp ile | Microsoft Docs"
description: "Nasıl kullanılacağını Vamp yalancı yayın Hizmetleri ve akıllı trafik bir Azure kapsayıcı hizmeti DC/OS kümesinde filtreleme Uygula"
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
ms.openlocfilehash: 4a20091b59f2643ea71cce99c159a5075706e35d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="483f0-103">Bir Azure kapsayıcı hizmeti DC/OS kümesinde yalancı yayın mikro Vamp ile</span><span class="sxs-lookup"><span data-stu-id="483f0-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="483f0-104">Bu kılavuzda, biz Vamp Azure kapsayıcı hizmeti DC/OS kümesi ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="483f0-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="483f0-105">Biz yalancı Vamp demo hizmeti "sava" yayın ve akıllı trafik filtreleme uygulayarak bir uyumsuzluk Firefox ile hizmetinin çözün.</span><span class="sxs-lookup"><span data-stu-id="483f0-105">We canary release the Vamp demo service "sava", and then resolve an incompatibility of the service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="483f0-106">Bu kılavuzda Vamp bir DC/OS kümesinde çalışır, ancak ayrıca Vamp Kubernetes ile orchestrator kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="483f0-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as the orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="483f0-107">Yalancı serbest bırakır ve Vamp hakkında</span><span class="sxs-lookup"><span data-stu-id="483f0-107">About canary releases and Vamp</span></span>


<span data-ttu-id="483f0-108">[Yalancı serbest](https://martinfowler.com/bliki/CanaryRelease.html) olan Netflix, Facebook ve Spotify gibi yenilikçi kuruluşlar tarafından benimsenen akıllı Dağıtım stratejisi.</span><span class="sxs-lookup"><span data-stu-id="483f0-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="483f0-109">Sorunları azaltır, ağ güvenliği tanıtır ve yenilik artırır bulunduğundan, mantıklı bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="483f0-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="483f0-110">Bu nedenle neden tüm şirketlerin kullanmadığınız?</span><span class="sxs-lookup"><span data-stu-id="483f0-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="483f0-111">CI/CD ardışık yalancı stratejileri içerecek şekilde genişletme karmaşıklık ekler ve kapsamlı bir devops bilgi ve deneyimlerine gerektirir.</span><span class="sxs-lookup"><span data-stu-id="483f0-111">Extending a CI/CD pipeline to include canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="483f0-112">Daha küçük şirket ve kuruluş aynı şekilde bile çalışmaya başlamadan önce engellemek için yeterli olur.</span><span class="sxs-lookup"><span data-stu-id="483f0-112">That’s enough to block smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="483f0-113">[Vamp](http://vamp.io/) bu geçişi kolaylaştırmak ve canary hale getirmek için tasarlanmış bir açık kaynak sistemi serbest bırakma, tercih edilen kapsayıcı Zamanlayıcı Özellikleri.</span><span class="sxs-lookup"><span data-stu-id="483f0-113">[Vamp](http://vamp.io/) is an open-source system designed to ease this transition and bring canary releasing features to your preferred container scheduler.</span></span> <span data-ttu-id="483f0-114">Yüzde tabanlı sürülmeleri vamp'ın yalancı işlevselliği gider.</span><span class="sxs-lookup"><span data-stu-id="483f0-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="483f0-115">Trafik filtre ve çok çeşitli koşullar, örneğin hedef belirli kullanıcılar, IP aralıkları veya cihazlar için bölme.</span><span class="sxs-lookup"><span data-stu-id="483f0-115">Traffic can be filtered and split on a wide range of conditions, for example to target specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="483f0-116">Vamp izler ve performans ölçümleri, gerçek verilerine dayalı Otomasyon izin vermeyi analiz eder.</span><span class="sxs-lookup"><span data-stu-id="483f0-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="483f0-117">Otomatik geri alma işlemi hatalarla ayarlayın veya bireysel hizmet çeşitleri yük veya gecikme göre ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="483f0-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="483f0-118">Azure kapsayıcı hizmeti DC/OS ile ayarlama</span><span class="sxs-lookup"><span data-stu-id="483f0-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="483f0-119">[DC/OS kümesi dağıtma](container-service-deployment.md) bir ana ve varsayılan boyutunun iki aracı ile.</span><span class="sxs-lookup"><span data-stu-id="483f0-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="483f0-120">[SSH tüneli oluşturma](../container-service-connect.md) DC/OS kümesine bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="483f0-120">[Create an SSH tunnel](../container-service-connect.md) to connect to the DC/OS cluster.</span></span> <span data-ttu-id="483f0-121">Bu makale, tünel yerel bağlantı noktası 80 üzerinde kümeye varsayar.</span><span class="sxs-lookup"><span data-stu-id="483f0-121">This article assumes that you tunnel to the cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="483f0-122">Vamp ayarlayın</span><span class="sxs-lookup"><span data-stu-id="483f0-122">Set up Vamp</span></span>

<span data-ttu-id="483f0-123">Çalışan DC/OS kümesine sahip olduğunuza göre DC/OS UI (http://localhost:80) Vamp yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="483f0-123">Now that you have a running DC/OS cluster, you can install Vamp from the DC/OS UI (http://localhost:80).</span></span> 

![DC/OS Kullanıcı Arabirimi](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="483f0-125">Yükleme, iki aşamada yapılır:</span><span class="sxs-lookup"><span data-stu-id="483f0-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="483f0-126">**Elasticsearch dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="483f0-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="483f0-127">Ardından **Vamp dağıtmak** Vamp DC/OS universe paketi yükleyerek.</span><span class="sxs-lookup"><span data-stu-id="483f0-127">Then **deploy Vamp** by installing the Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="483f0-128">Elasticsearch dağıtma</span><span class="sxs-lookup"><span data-stu-id="483f0-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="483f0-129">Vamp Elasticsearch ölçümleri toplama ve toplama için gerektirir.</span><span class="sxs-lookup"><span data-stu-id="483f0-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="483f0-130">Kullanabileceğiniz [magneticio Docker görüntüleri](https://hub.docker.com/r/magneticio/elastic/) uyumlu Vamp Elasticsearch yığın dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="483f0-130">You can use the [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) to deploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="483f0-131">DC/OS kullanıcı arabirimini Git **Hizmetleri** tıklatıp **hizmeti Dağıt**.</span><span class="sxs-lookup"><span data-stu-id="483f0-131">In the DC/OS UI, go to **Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="483f0-132">Seçin **JSON modu** gelen **yeni hizmeti Dağıt** açılır.</span><span class="sxs-lookup"><span data-stu-id="483f0-132">Select **JSON mode** from the **Deploy New Service** pop-up.</span></span>

  ![JSON modu seçin](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="483f0-134">Aşağıdaki JSON öğesini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="483f0-134">Paste in the following JSON.</span></span> <span data-ttu-id="483f0-135">Bu yapılandırma, 1 GB RAM ve temel sistem durumu denetimi Elasticsearch bağlantı noktası ile kapsayıcı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="483f0-135">This configuration runs the container with 1 GB of RAM and a basic health check on the Elasticsearch port.</span></span>
  
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
  

3. <span data-ttu-id="483f0-136">Tıklatın **dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="483f0-136">Click **Deploy**.</span></span>

  <span data-ttu-id="483f0-137">DC/OS Elasticsearch kapsayıcı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="483f0-137">DC/OS deploys the Elasticsearch container.</span></span> <span data-ttu-id="483f0-138">Üzerinde ilerleme durumunu izleyebilirsiniz **Hizmetleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="483f0-138">You can track progress on the **Services** page.</span></span>  

  ![e dağıtabilir? Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="483f0-140">Vamp dağıtma</span><span class="sxs-lookup"><span data-stu-id="483f0-140">Deploy Vamp</span></span>

<span data-ttu-id="483f0-141">Olarak Elasticsearch raporları bir kez **çalıştıran**, DC/OS Universe Vamp paket ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="483f0-141">Once Elasticsearch reports as **Running**, you can add the Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="483f0-142">Git **Universe** arayın ve **vamp**.</span><span class="sxs-lookup"><span data-stu-id="483f0-142">Go to **Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="483f0-143">![DC/OS universe üzerinde vamp](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="483f0-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="483f0-144">Tıklatın **yükleme** vamp yanındaki paketini bulun ve seçin **gelişmiş yükleme**.</span><span class="sxs-lookup"><span data-stu-id="483f0-144">Click **install** next to the vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="483f0-145">Aşağı kaydırın ve aşağıdaki elasticsearch URL'yi girin: `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="483f0-145">Scroll down and enter the following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Elasticsearch URL'sini girin](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="483f0-147">Tıklatın **gözden geçirin ve yükleyin**, ardından **yükleme** dağıtımı başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="483f0-147">Click **Review and Install**, then click **Install** to start the deployment.</span></span>  

  <span data-ttu-id="483f0-148">DC/OS gerekli tüm Vamp bileşenlerini dağıtır.</span><span class="sxs-lookup"><span data-stu-id="483f0-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="483f0-149">Üzerinde ilerleme durumunu izleyebilirsiniz **Hizmetleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="483f0-149">You can track progress on the **Services** page.</span></span>
  
  ![Vamp universe paketi olarak dağıtma](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="483f0-151">Dağıtım tamamlandıktan sonra Vamp UI erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="483f0-151">Once deployment has completed, you can access the Vamp UI:</span></span>

  ![DC/OS vamp hizmeti](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![UI vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="483f0-154">İlk hizmetiniz dağıtma</span><span class="sxs-lookup"><span data-stu-id="483f0-154">Deploy your first service</span></span>

<span data-ttu-id="483f0-155">Bu Vamp çalışır durumda artık şeması hizmetinden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="483f0-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="483f0-156">En basit biçimiyle içinde bir [Vamp şeması](http://vamp.io/documentation/using-vamp/blueprints/) uç noktaları (ağ geçidi), kümeler ve Hizmetleri dağıtmak için açıklar.</span><span class="sxs-lookup"><span data-stu-id="483f0-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes the endpoints (gateways), clusters, and services to deploy.</span></span> <span data-ttu-id="483f0-157">Vamp aynı hizmetin farklı türevleri yalancı serbest bırakma veya bir mantıksal gruplar halinde gruplandırmak için kümeler kullanır / B testi.</span><span class="sxs-lookup"><span data-stu-id="483f0-157">Vamp uses clusters to group different variants of the same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="483f0-158">Bu senaryo adlı örnek bir tek yapılı uygulama kullanır [ **sava**](https://github.com/magneticio/sava), sürüm 1.0 olduğu.</span><span class="sxs-lookup"><span data-stu-id="483f0-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="483f0-159">Monolith Docker Hub magneticio/sava:1.0.0 altında olan bir Docker kapsayıcısı paketlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="483f0-159">The monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="483f0-160">Uygulamanın normal olarak bağlantı noktası 8080 üzerinde çalışır, ancak bu durumda bağlantı 9050 altında kullanıma sunmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="483f0-160">The app normally runs on port 8080, but you want to expose it under port 9050 in this case.</span></span> <span data-ttu-id="483f0-161">Basit şeması kullanarak Vamp aracılığıyla uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="483f0-161">Deploy the app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="483f0-162">Git **dağıtımları**.</span><span class="sxs-lookup"><span data-stu-id="483f0-162">Go to **Deployments**.</span></span>

2. <span data-ttu-id="483f0-163">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="483f0-163">Click **Add**.</span></span>

3. <span data-ttu-id="483f0-164">Aşağıdaki şeması YAML yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="483f0-164">Paste in the following blueprint YAML.</span></span> <span data-ttu-id="483f0-165">Bu şeması sizi bir sonraki adımda değiştirmek yalnızca bir hizmet değişken ile tek bir küme içerir:</span><span class="sxs-lookup"><span data-stu-id="483f0-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster to create
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="483f0-166">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="483f0-166">Click **Save**.</span></span> <span data-ttu-id="483f0-167">Vamp dağıtımı başlatır.</span><span class="sxs-lookup"><span data-stu-id="483f0-167">Vamp initiates the deployment.</span></span>

<span data-ttu-id="483f0-168">Dağıtım listelendiğini **dağıtımları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="483f0-168">The deployment is listed on the **Deployments** page.</span></span> <span data-ttu-id="483f0-169">Dağıtım durumunu izlemek için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="483f0-169">Click the deployment to monitor its status.</span></span>

![UI Sava dağıtma - vamp](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Kullanıcı arabiriminde Vamp Sava hizmeti](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="483f0-172">İki ağ geçidi oluşturulur, hangi listelendiğini **ağ geçitleri** sayfa:</span><span class="sxs-lookup"><span data-stu-id="483f0-172">Two gateways are created, which are listed on the **Gateways** page:</span></span>

* <span data-ttu-id="483f0-173">çalışan hizmetin (bağlantı noktası 9050) erişmek için tutarlı bir uç noktası</span><span class="sxs-lookup"><span data-stu-id="483f0-173">a stable endpoint to access the running service (port 9050)</span></span> 
* <span data-ttu-id="483f0-174">bir Vamp yönetilen iç ağ geçidi (daha sonra bu ağ geçidi hakkında daha fazla).</span><span class="sxs-lookup"><span data-stu-id="483f0-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![UI - sava ağ geçitleri vamp](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="483f0-176">Sava hizmeti şimdi dağıtmış olan ancak Azure yük dengeleyici, trafik henüz iletmek için bilmiyor olduğundan, dışarıdan erişemez.</span><span class="sxs-lookup"><span data-stu-id="483f0-176">The sava service has now deployed, but you can’t access it externally because the Azure Load Balancer doesn’t know to forward traffic to it yet.</span></span> <span data-ttu-id="483f0-177">Hizmete erişmek için Azure ağ yapılandırmasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="483f0-177">To access the service, update the Azure networking configuration.</span></span>


## <a name="update-the-azure-network-configuration"></a><span data-ttu-id="483f0-178">Azure ağ yapılandırmasını güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="483f0-178">Update the Azure network configuration</span></span>

<span data-ttu-id="483f0-179">Vamp kararlı bir uç nokta bağlantı noktası 9050 gösterme DC/OS Aracısı düğümlerde sava hizmetini dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="483f0-179">Vamp deployed the sava service on the DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="483f0-180">DC/OS kümesi dışında hizmetinden erişmek için Küme dağıtımı Azure ağ yapılandırmasında aşağıdaki değişiklikleri yapın:</span><span class="sxs-lookup"><span data-stu-id="483f0-180">To access the service from outside the DC/OS cluster, make the following changes to the Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="483f0-181">**Azure yük dengeleyici yapılandırmanız** aracıları için (adlı kaynak **dcos-aracı-lb-xxxx**) ile bir durum araştırması ve sava örneklerine 9050 numaralı bağlantı noktasında trafik iletmek için bir kural.</span><span class="sxs-lookup"><span data-stu-id="483f0-181">**Configure the Azure Load Balancer** for the agents (the resource named **dcos-agent-lb-xxxx**) with a health probe and a rule to forward traffic on port 9050 to the sava instances.</span></span> 

2. <span data-ttu-id="483f0-182">**Ağ güvenlik grubu güncelleştirme** ortak aracılar için (adlı kaynak **XXXX-aracı-genel-nsg-XXXX**) bağlantı noktası 9050 trafiğine izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="483f0-182">**Update the network security group** for the public agents (the resource named **XXXX-agent-public-nsg-XXXX**) to allow traffic on port 9050.</span></span>

<span data-ttu-id="483f0-183">Azure Portalı'nı kullanarak bu görevleri tamamlamak ayrıntılı adımlar için bkz: [Azure kapsayıcı hizmeti uygulamanın genel erişimi etkinleştirme](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="483f0-183">For detailed steps to complete these tasks using the Azure portal, see [Enable public access to an Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="483f0-184">Bağlantı noktasını 9050 tüm bağlantı noktası ayarlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="483f0-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="483f0-185">Her şeyi oluşturulduktan sonra Git **genel bakış** dikey DC/OS Aracısı Yük Dengeleyici (adlı kaynak **dcos-aracı-lb-xxxx**).</span><span class="sxs-lookup"><span data-stu-id="483f0-185">Once everything has been created, go to the **Overview** blade of the DC/OS agent load balancer (the resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="483f0-186">Bul **genel IP adresi**ve adres 9050 noktasındaki sava erişmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="483f0-186">Find the **Public IP address**, and use the address to access sava at port 9050.</span></span>

![Azure portal - get genel IP adresi](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![Sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="483f0-189">Yalancı yayın çalıştırın</span><span class="sxs-lookup"><span data-stu-id="483f0-189">Run a canary release</span></span>

<span data-ttu-id="483f0-190">İstediğiniz bu uygulamanın üretime yalancı sürüm için yeni bir sürümü olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="483f0-190">Suppose you have a new version of this application that you want to canary release into production.</span></span> <span data-ttu-id="483f0-191">Magneticio/sava:1.1.0 kapsayıcılı olması ve başlamaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="483f0-191">You have it containerized as magneticio/sava:1.1.0 and are ready to go.</span></span> <span data-ttu-id="483f0-192">Vamp yeni hizmetler çalışan dağıtımının kolayca eklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="483f0-192">Vamp lets you easily add new services to the running deployment.</span></span> <span data-ttu-id="483f0-193">"Birleştirilmiş" hizmetlerin kümedeki varolan hizmetleri yanında dağıtılan ve Ağırlık % 0 olarak atanmış.</span><span class="sxs-lookup"><span data-stu-id="483f0-193">These "merged" services are deployed alongside the existing services in the cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="483f0-194">Trafik dağılımı ayarlamak kadar hiçbir trafik yeni birleştirilmiş bir hizmete yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="483f0-194">No traffic is routed to a newly merged service until you adjust the traffic distribution.</span></span> <span data-ttu-id="483f0-195">Ağırlık kaydırıcıyı Vamp kullanıcı arabiriminde artımlı ayarlamalar (yalancı sürüm) ya da anlık bir geri alma için izin vererek bu dağıtım üzerinde tam denetim verir.</span><span class="sxs-lookup"><span data-stu-id="483f0-195">The weight slider in the Vamp UI gives you complete control over the distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="483f0-196">Yeni bir hizmet değişken birleştirme</span><span class="sxs-lookup"><span data-stu-id="483f0-196">Merge a new service variant</span></span>

<span data-ttu-id="483f0-197">Çalışan dağıtımının yeni sava 1.1 hizmetiyle birleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="483f0-197">To merge the new sava 1.1 service with the running deployment:</span></span>

1. <span data-ttu-id="483f0-198">Vamp UI'ı tıklatın **planlar**.</span><span class="sxs-lookup"><span data-stu-id="483f0-198">In the Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="483f0-199">Tıklatın **Ekle** ve aşağıdaki şeması YAML yapıştırın: var olan küme içinde (sava_cluster) dağıtmak için bir yeni hizmet değişken (sava: 1.1.0) bu şeması açıklar.</span><span class="sxs-lookup"><span data-stu-id="483f0-199">Click **Add** and paste in the following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) to deploy within the existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster to update
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint to update
  ```
  
3. <span data-ttu-id="483f0-200">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="483f0-200">Click **Save**.</span></span> <span data-ttu-id="483f0-201">Şeması depolanır ve listelenen **planlar** sayfası.</span><span class="sxs-lookup"><span data-stu-id="483f0-201">The blueprint is stored and listed on the **Blueprints** page.</span></span>

4. <span data-ttu-id="483f0-202">Sava: 1.1 şeması Eylem menüsünde açıp tıklatın **birleştirilecek**.</span><span class="sxs-lookup"><span data-stu-id="483f0-202">Open the action menu on the sava:1.1 blueprint and click **Merge to**.</span></span>

  ![UI - planlar vamp](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="483f0-204">Seçin **sava** dağıtım ve tıklatın **birleştirme**.</span><span class="sxs-lookup"><span data-stu-id="483f0-204">Select the **sava** deployment and click **Merge**.</span></span>

  ![UI - dağıtım için birleştirme şeması vamp](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="483f0-206">Vamp dağıtır sava: 1.0.0 yanında şeması açıklanan yeni sava: 1.1.0 hizmeti değişken **sava_cluster** çalışan dağıtım.</span><span class="sxs-lookup"><span data-stu-id="483f0-206">Vamp deploys the new sava:1.1.0 service variant described in the blueprint alongside sava:1.0.0 in the **sava_cluster** of the running deployment.</span></span> 

![UI - güncelleştirilmiş sava dağıtım vamp](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="483f0-208">**Sava_cluster/sava/webport** ağ geçidi (küme uç noktası) de güncelleştirilir, yeni dağıtılan sava: 1.1.0 bir yol ekleme.</span><span class="sxs-lookup"><span data-stu-id="483f0-208">The **sava/sava_cluster/webport** gateway (the cluster endpoint) is also updated, adding a route to the newly deployed sava:1.1.0.</span></span> <span data-ttu-id="483f0-209">Bu noktada, hiçbir trafik burada yönlendirilen ( **ağırlık** %0 olarak ayarlanır).</span><span class="sxs-lookup"><span data-stu-id="483f0-209">At this point, no traffic is routed here (the **WEIGHT** is set to 0%).</span></span>

![UI - küme ağ geçidi vamp](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="483f0-211">Yalancı sürüm</span><span class="sxs-lookup"><span data-stu-id="483f0-211">Canary release</span></span>

<span data-ttu-id="483f0-212">Her iki aynı kümede dağıtılan sava sürümleriyle taşıyarak aralarındaki trafik dağıtım Ayarla **ağırlık** kaydırıcı.</span><span class="sxs-lookup"><span data-stu-id="483f0-212">With both versions of sava deployed in the same cluster, adjust the distribution of traffic between them by moving the **WEIGHT** slider.</span></span>

1. <span data-ttu-id="483f0-213">Tıklatın ![Vamp UI - Düzenle](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) yanına **ağırlık**.</span><span class="sxs-lookup"><span data-stu-id="483f0-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT**.</span></span>

2. <span data-ttu-id="483f0-214">% 50 / % 50'ye tıklayın ağırlık dağıtımı ayarlayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="483f0-214">Set the weight distribution to 50%/50% and click **Save**.</span></span>

  ![UI - ağ geçidi ağırlık kaydırıcı vamp](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="483f0-216">Tarayıcınıza geri dönün ve birkaç kere sava sayfayı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="483f0-216">Go back to your browser and refresh the sava page a few more times.</span></span> <span data-ttu-id="483f0-217">Sava uygulamayı şimdi sava: 1.0 sayfa sava: 1.1 sayfa arasında geçiş yapar.</span><span class="sxs-lookup"><span data-stu-id="483f0-217">The sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![değişen sava1.0 ve sava1.1 Hizmetleri](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="483f0-219">Bu değişim sayfasının en iyi "Incognito" veya "Anonim" modu tarayıcınızın statik varlıklarını önbelleğe alma nedeniyle çalışır.</span><span class="sxs-lookup"><span data-stu-id="483f0-219">This alternation of the page works best with the "Incognito" or “Anonymous” mode of your browser because of the caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="483f0-220">Trafik filtre</span><span class="sxs-lookup"><span data-stu-id="483f0-220">Filter traffic</span></span>

<span data-ttu-id="483f0-221">Dağıtımdan sonra bir uyumsuzluk sava: 1.1.0 nedenleri Firefox tarayıcılarda sorunları görüntülemek içinde bulunan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="483f0-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="483f0-222">Gelen trafiği filtrelemek ve bilinen kararlı sava: 1.0.0 için tüm Firefox kullanıcıları geri doğrudan Vamp ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="483f0-222">You can set Vamp to filter incoming traffic and direct all Firefox users back to the known stable sava:1.0.0.</span></span> <span data-ttu-id="483f0-223">Başka bir herkes geliştirilmiş sava: 1.1.0 avantajlarından devam ederken bu filtre kesintisi Firefox kullanıcılar için anında çözümler.</span><span class="sxs-lookup"><span data-stu-id="483f0-223">This filter instantly resolves the disruption for Firefox users, while everybody else continues to enjoy the benefits of the improved sava:1.1.0.</span></span>

<span data-ttu-id="483f0-224">Kullanır vamp **koşullar** filtre trafiği bir ağ geçidi yollar arasında.</span><span class="sxs-lookup"><span data-stu-id="483f0-224">Vamp uses **conditions** to filter traffic between routes in a gateway.</span></span> <span data-ttu-id="483f0-225">Trafik ilk filtre ve her yolu uygulanan koşullar göre yönlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="483f0-225">Traffic is first filtered and directed according to the conditions applied to each route.</span></span> <span data-ttu-id="483f0-226">Tüm kalan trafik, ağ geçidi ağırlığı ayarına göre dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="483f0-226">All remaining traffic is distributed according to the gateway weight setting.</span></span>

<span data-ttu-id="483f0-227">Tüm Firefox kullanıcıları filtrelemek ve eski sava: 1.0.0 yönlendirmek için bir koşul oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="483f0-227">You can create a condition to filter all Firefox users and direct them to the old sava:1.0.0:</span></span>

1. <span data-ttu-id="483f0-228">Sava/sava_cluster/webport üzerinde **ağ geçitleri** sayfasında, ![Vamp UI - Düzenle](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) eklemek için bir **KOŞULU** rota sava/sava_cluster/sava:1.0.0/webport için.</span><span class="sxs-lookup"><span data-stu-id="483f0-228">On the sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to add a **CONDITION** to the route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="483f0-229">Koşul girin **kullanıcı aracısı Firefox ==** tıklatıp ![Vamp UI - Kaydet](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="483f0-229">Enter the condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="483f0-230">Vamp varsayılan gücü koşuluyla %0 ekler.</span><span class="sxs-lookup"><span data-stu-id="483f0-230">Vamp adds the condition with a default strength of 0%.</span></span> <span data-ttu-id="483f0-231">Trafik filtreleme başlatmak için koşul gücü ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="483f0-231">To start filtering traffic, you need to adjust the condition strength.</span></span>

3. <span data-ttu-id="483f0-232">Tıklatın ![Vamp UI - Düzenle](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) değiştirmek için **gücü** durumuna uygulanır.</span><span class="sxs-lookup"><span data-stu-id="483f0-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to change the **STRENGTH** applied to the condition.</span></span>
 
4. <span data-ttu-id="483f0-233">Ayarlama **gücü** % 100 ve tıklatın ![Vamp UI - Kaydet](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="483f0-233">Set the **STRENGTH** to 100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) to save.</span></span>

  <span data-ttu-id="483f0-234">Vamp şimdi sava: 1.0.0 durumuna (tüm Firefox kullanıcılar) ile eşleşen tüm trafik gönderir.</span><span class="sxs-lookup"><span data-stu-id="483f0-234">Vamp now sends all traffic matching the condition (all Firefox users) to sava:1.0.0.</span></span>

  ![UI vamp - ağ geçidi koşul Uygula](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="483f0-236">Son olarak, tüm kalan trafiği (tüm Firefox olmayan kullanıcılar) yeni sava: 1.1.0 göndermek için ağ geçidi ağırlığı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="483f0-236">Finally, adjust the gateway weight to send all remaining traffic (all non-Firefox users) to the new sava:1.1.0.</span></span> <span data-ttu-id="483f0-237">Tıklatın ![Vamp UI - Düzenle](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) yanına **ağırlık** ve Ağırlık dağıtımı % 100 rota sava/sava_cluster/sava:1.1.0/webport yönergelerine uygun şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="483f0-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT** and set the weight distribution so 100% is directed to the route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="483f0-238">Koşul tarafından filtrelenmiş olmayan tüm trafiği şimdi yeni sava: 1.1.0 yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="483f0-238">All traffic not filtered by the condition is now directed to the new sava:1.1.0.</span></span>

6. <span data-ttu-id="483f0-239">Eylem filtresinde görmek için iki farklı tarayıcılar (bir Firefox ve başka bir tarayıcı) açın ve sava hizmet hem de erişin.</span><span class="sxs-lookup"><span data-stu-id="483f0-239">To see the filter in action, open two different browsers (one Firefox and one other browser) and access the sava service from both.</span></span> <span data-ttu-id="483f0-240">Diğer tüm tarayıcılar sava: 1.1.0 yönlendirilir sırada tüm Firefox istekleri sava: 1.0.0 gönderilir.</span><span class="sxs-lookup"><span data-stu-id="483f0-240">All Firefox requests are sent to sava:1.0.0, while all other browsers are directed to sava:1.1.0.</span></span>

  ![UI - filtre trafiği vamp](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="483f0-242">Özetle</span><span class="sxs-lookup"><span data-stu-id="483f0-242">Summing up</span></span>

<span data-ttu-id="483f0-243">Bu makalede bir giriş Vamp bir DC/OS kümesinde oluştu.</span><span class="sxs-lookup"><span data-stu-id="483f0-243">This article was a quick introduction to Vamp on a DC/OS cluster.</span></span> <span data-ttu-id="483f0-244">Yeni başlayanlar Vamp aldı ve, Azure kapsayıcı hizmeti DC/OS üzerinde çalışan küme, hizmet Vamp şeması ile dağıtılan ve (ağ geçidi) sunulan uç noktada erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="483f0-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at the exposed endpoint (gateway).</span></span>

<span data-ttu-id="483f0-245">Biz de güçlü özelliklerinden bazıları Vamp üzerinde işlemdeki: çalışan dağıtımına yeni bir hizmet değişken birleştirme ve artımlı olarak Tanıtımı sonra bilinen uyumsuzluğu gidermek için trafik filtreleme.</span><span class="sxs-lookup"><span data-stu-id="483f0-245">We also touched on some powerful features of Vamp:  merging a new service variant to the running deployment and introducing it incrementally, then filtering traffic to resolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="483f0-246">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="483f0-246">Next steps</span></span>

* <span data-ttu-id="483f0-247">Vamp Eylemler ile yönetme hakkında bilgi edinin [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="483f0-247">Learn about managing Vamp actions through the [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="483f0-248">Node.js içinde Vamp Otomasyon betikleri oluşturmak ve bunları olarak çalıştırma [Vamp iş akışları](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="483f0-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="483f0-249">Bkz: ek [VAMP öğreticileri](http://vamp.io/documentation/tutorials/overview/).</span><span class="sxs-lookup"><span data-stu-id="483f0-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

