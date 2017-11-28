---
title: "aaaLoad Bakiye Azure Kubernetes kapsayıcılarında | Microsoft Docs"
description: "Harici olarak bağlayın ve Azure kapsayıcı Hizmeti'nde Kubernetes kümedeki birden çok kapsayıcı arasında Yük Dengelemesi."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, mikro hizmetler, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="91400-104">Azure kapsayıcı hizmeti Kubernetes kümede Yük Dengelemesi kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="91400-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="91400-105">Bu makalede, Azure kapsayıcı Hizmeti'nde Kubernetes kümedeki dengelemesini tanıtılır.</span><span class="sxs-lookup"><span data-stu-id="91400-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="91400-106">Yük Dengeleme hello hizmeti için harici olarak erişilebilir bir IP adresi sağlar ve ağ trafiğini aracısını sanal makineleri çalıştıran hello pod'ları arasında dağıtır.</span><span class="sxs-lookup"><span data-stu-id="91400-106">Load balancing provides an externally accessible IP address for hello service and distributes network traffic among hello pods running in agent VMs.</span></span>

<span data-ttu-id="91400-107">Kubernetes hizmet toouse ayarlayabilirsiniz [Azure yük dengeleyici](../../load-balancer/load-balancer-overview.md) toomanage dış (TCP) ağ trafiği.</span><span class="sxs-lookup"><span data-stu-id="91400-107">You can set up a Kubernetes service toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage external network (TCP) traffic.</span></span> <span data-ttu-id="91400-108">Ek bir yapılandırma olmadan Yük Dengeleme ve HTTP veya HTTPS trafiği veya daha Gelişmiş senaryolar yönlendirme mümkündür.</span><span class="sxs-lookup"><span data-stu-id="91400-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91400-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="91400-109">Prerequisites</span></span>
* <span data-ttu-id="91400-110">[Kubernetes küme dağıtma](container-service-kubernetes-walkthrough.md) Azure kapsayıcı Hizmeti'nde</span><span class="sxs-lookup"><span data-stu-id="91400-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="91400-111">[İstemci bağlantı](../container-service-connect.md) tooyour küme</span><span class="sxs-lookup"><span data-stu-id="91400-111">[Connect your client](../container-service-connect.md) tooyour cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="91400-112">Azure yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="91400-112">Azure load balancer</span></span>

<span data-ttu-id="91400-113">Varsayılan olarak, Azure kapsayıcı Hizmeti'nde dağıtılan Kubernetes küme hello Aracısı VM'ler için bir Internet'e yönelik Azure yük dengeleyici içerir.</span><span class="sxs-lookup"><span data-stu-id="91400-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for hello agent VMs.</span></span> <span data-ttu-id="91400-114">(Ayrı yük dengeleyici kaynak hello Yöneticisi VM'ler için yapılandırılır.) Azure yük dengeleyici katman 4 yük dengeleyici ' dir.</span><span class="sxs-lookup"><span data-stu-id="91400-114">(A separate load balancer resource is configured for hello master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="91400-115">Şu anda hello yük dengeleyici Kubernetes içinde yalnızca TCP trafiğini destekler.</span><span class="sxs-lookup"><span data-stu-id="91400-115">Currently, hello load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="91400-116">Kubernetes hizmet oluşturulurken hello Azure yük dengeleyici tooallow erişim toohello hizmeti otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91400-116">When creating a Kubernetes service, you can automatically configure hello Azure load balancer tooallow access toohello service.</span></span> <span data-ttu-id="91400-117">tooconfigure hello yük dengeleyici, kümesi hello hizmet `type` çok`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="91400-117">tooconfigure hello load balancer, set hello service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="91400-118">Aracı VM'ler (ve tersi yanıt trafiği için), bir ortak IP adresi ve bağlantı noktası numarası gelen hizmet trafiği toohello özel IP adresleri ve bağlantı noktası numaralarını hello pod'ları bir kural toomap Hello yük dengeleyici oluşturur.</span><span class="sxs-lookup"><span data-stu-id="91400-118">hello load balancer creates a rule toomap a public IP address and port number of incoming service traffic toohello private IP addresses and port numbers of hello pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="91400-119">Nasıl tooset hello Kubernetes hizmet gösteren iki örnek verilmiştir `type` çok`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="91400-119">Following are two examples showing how tooset hello Kubernetes service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="91400-120">(Artık gereksinim duyduğunuzda çalışırken hello örnekler sonra hello dağıtımları silin.)</span><span class="sxs-lookup"><span data-stu-id="91400-120">(After trying hello examples, delete hello deployments if you no longer need them.)</span></span>

### <a name="example-use-hello-kubectl-expose-command"></a><span data-ttu-id="91400-121">Örnek: Kullanım hello `kubectl expose` komutu</span><span class="sxs-lookup"><span data-stu-id="91400-121">Example: Use hello `kubectl expose` command</span></span> 
<span data-ttu-id="91400-122">Merhaba [Kubernetes izlenecek](container-service-kubernetes-walkthrough.md) nasıl bir örnek içerir tooexpose hello hizmetiyle `kubectl expose` komutu ve onun `--type=LoadBalancer` bayrağı.</span><span class="sxs-lookup"><span data-stu-id="91400-122">hello [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how tooexpose a service with hello `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="91400-123">Merhaba adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="91400-123">Here are hello steps :</span></span>

1. <span data-ttu-id="91400-124">Yeni bir kapsayıcı dağıtımı başlatın.</span><span class="sxs-lookup"><span data-stu-id="91400-124">Start a new container deployment.</span></span> <span data-ttu-id="91400-125">Örneğin, yeni bir dağıtım adlı komut başlatır aşağıdaki hello `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="91400-125">For example, hello following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="91400-126">Merhaba dağıtım hello Docker görüntü hello Nginx web sunucusu için temel üç kapsayıcı oluşur.</span><span class="sxs-lookup"><span data-stu-id="91400-126">hello deployment consists of three containers based on hello Docker image for hello Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="91400-127">Merhaba kapsayıcılara çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="91400-127">Verify that hello containers are running.</span></span> <span data-ttu-id="91400-128">Örneğin, Merhaba kapsayıcılara ile sorgulama `kubectl get pods`, çıktı benzer toohello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="91400-128">For example, if you query for hello containers with `kubectl get pods`, you see output similar toohello following:</span></span>

    ![Nginx kapsayıcısı alma](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="91400-130">çalıştırma tooconfigure hello yük dengeleyici tooaccept dış trafiğin toohello dağıtımı, `kubectl expose` ile `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="91400-130">tooconfigure hello load balancer tooaccept external traffic toohello deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="91400-131">Merhaba aşağıdaki komutu hello Nginx sunucu bağlantı noktası 80 üzerinde sunar:</span><span class="sxs-lookup"><span data-stu-id="91400-131">hello following command exposes hello Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="91400-132">Tür `kubectl get svc` toosee hello hello kümedeki hello hizmetlerinin durumunu.</span><span class="sxs-lookup"><span data-stu-id="91400-132">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="91400-133">Merhaba yük dengeleyici hello kuralı yapılandırırken hello `EXTERNAL-IP` Merhaba hizmet olarak görünür. `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="91400-133">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello service appears as `<pending>`.</span></span> <span data-ttu-id="91400-134">Birkaç dakika sonra hello dış IP adresi yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="91400-134">After a few minutes, hello external IP address is configured:</span></span> 

    ![Azure yük dengeleyici yapılandırma](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="91400-136">Merhaba hizmet hello dış IP adresine erişebildiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="91400-136">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="91400-137">Örneğin, gösterilen bir web tarayıcısı toohello IP adresini açın.</span><span class="sxs-lookup"><span data-stu-id="91400-137">For example, open a web browser toohello IP address shown.</span></span> <span data-ttu-id="91400-138">Merhaba tarayıcı Merhaba kapsayıcılara birinde çalışan hello Nginx web sunucusu gösterir.</span><span class="sxs-lookup"><span data-stu-id="91400-138">hello browser shows hello Nginx web server running in one of hello containers.</span></span> <span data-ttu-id="91400-139">Veya, çalışma hello `curl` veya `wget` komutu.</span><span class="sxs-lookup"><span data-stu-id="91400-139">Or, run hello `curl` or `wget` command.</span></span> <span data-ttu-id="91400-140">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="91400-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="91400-141">Aşağıdakine benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="91400-141">You should see output similar to:</span></span>

    ![Erişim Nginx curl ile](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="91400-143">hello Azure yük dengeleyici, Git toohello toosee hello yapılandırmasını [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91400-143">toosee hello configuration of hello Azure load balancer, go toohello [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="91400-144">Merhaba kaynak grubu için kapsayıcı hizmeti kümesini bulun ve hello yük dengeleyici hello Aracısı VM'ler için seçin.</span><span class="sxs-lookup"><span data-stu-id="91400-144">Browse for hello resource group for your container service cluster, and select hello load balancer for hello agent VMs.</span></span> <span data-ttu-id="91400-145">Adını olması hello hello kapsayıcı hizmeti ile aynı.</span><span class="sxs-lookup"><span data-stu-id="91400-145">Its name should be hello same as hello container service.</span></span> <span data-ttu-id="91400-146">(Yok hello yük dengeleyici hello ana düğüm için seçin, bir adı içeren hello **ana lb**.)</span><span class="sxs-lookup"><span data-stu-id="91400-146">(Don't choose hello load balancer for hello master nodes, hello one whose name includes **master-lb**.)</span></span> 

    ![Kaynak grubundaki yük dengeleyici](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="91400-148">Merhaba yük dengeleyici yapılandırması, toosee hello ayrıntılarını tıklatın **Yük Dengeleme kuralları** ve yapılandırılan hello kuralının hello adı.</span><span class="sxs-lookup"><span data-stu-id="91400-148">toosee hello details of hello load balancer configuration, click **Load balancing rules** and hello name of hello rule that was configured.</span></span>

    ![Yük Dengeleyici kuralları](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a><span data-ttu-id="91400-150">Örnek: Belirtin `type: LoadBalancer` hello hizmet yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="91400-150">Example: Specify `type: LoadBalancer` in hello service configuration file</span></span>

<span data-ttu-id="91400-151">JSON veya YAML Kubernetes kapsayıcı uygulama dağıtırsanız [hizmet yapılandırma dosyası](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), aşağıdaki satırı toohello hizmet belirtimi hello ekleyerek bir dış yük dengeleyici belirtin:</span><span class="sxs-lookup"><span data-stu-id="91400-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding hello following line toohello service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="91400-152">Merhaba aşağıdaki adımları kullanın hello Kubernetes [Konuk örnek](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span><span class="sxs-lookup"><span data-stu-id="91400-152">hello following steps use hello Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="91400-153">Bu örnek, Redis ve PHP Docker görüntülerini temel çok katmanlı web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="91400-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="91400-154">Merhaba ön uç PHP sunucu hello Azure yük dengeleyici kullanan hello hizmet yapılandırma dosyasında belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91400-154">You can specify in hello service configuration file that hello frontend PHP server uses hello Azure load balancer.</span></span>

1. <span data-ttu-id="91400-155">Merhaba dosya indirme `guestbook-all-in-one.yaml` gelen [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="91400-155">Download hello file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="91400-156">Merhaba Gözat `spec` hello için `frontend` hizmet.</span><span class="sxs-lookup"><span data-stu-id="91400-156">Browse for hello `spec` for hello `frontend` service.</span></span>
3. <span data-ttu-id="91400-157">Merhaba satırı açıklamadan kaldırmasına `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="91400-157">Uncomment hello line `type: LoadBalancer`.</span></span>

    ![Yük Dengeleyici Hizmeti Yapılandırması](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="91400-159">Merhaba dosyasını kaydedin ve hello aşağıdaki komutu çalıştırarak hello uygulama dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="91400-159">Save hello file, and deploy hello app by running hello following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="91400-160">Tür `kubectl get svc` toosee hello hello kümedeki hello hizmetlerinin durumunu.</span><span class="sxs-lookup"><span data-stu-id="91400-160">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="91400-161">Merhaba yük dengeleyici hello kuralı yapılandırırken hello `EXTERNAL-IP` Merhaba, `frontend` hizmeti görünür olarak `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="91400-161">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="91400-162">Birkaç dakika sonra hello dış IP adresi yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="91400-162">After a few minutes, hello external IP address is configured:</span></span> 

    ![Azure yük dengeleyici yapılandırma](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="91400-164">Merhaba hizmet hello dış IP adresine erişebildiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="91400-164">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="91400-165">Örneğin, bir web tarayıcısı toohello dış IP adresi hello hizmetinin açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91400-165">For example, you can open a web browser toohello external IP address of hello service.</span></span>

    ![Dışarıdan erişim Konuk](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="91400-167">Konuk girişleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91400-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="91400-168">hello Azure yük dengeleyici, hello yük dengeleyici kaynak Gözat hello hello kümedeki toosee hello yapılandırmasını [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91400-168">toosee hello configuration of hello Azure load balancer, browse for hello load balancer resource for hello cluster in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="91400-169">Merhaba hello önceki örnekte adımlarına bakın.</span><span class="sxs-lookup"><span data-stu-id="91400-169">See hello steps in hello previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="91400-170">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="91400-170">Considerations</span></span>

* <span data-ttu-id="91400-171">Merhaba yük dengeleyici kuralı oluşturulmasını olur zaman uyumsuz olarak ve sağlanan hello dengeleyici hakkında bilgi hello hizmetin içinde yayımlanan `status.loadBalancer` alan.</span><span class="sxs-lookup"><span data-stu-id="91400-171">Creation of hello load balancer rule happens asynchronously, and information about hello provisioned balancer is published in hello service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="91400-172">Her hizmetin kendi hello yük dengeleyici sanal IP adresi otomatik olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="91400-172">Every service is automatically assigned its own virtual IP address in hello load balancer.</span></span>
* <span data-ttu-id="91400-173">Bir DNS adı tarafından tooreach hello yük dengeleyici istiyorsanız hello kuralındaki IP adresi için bir DNS adı, etki alanı hizmeti sağlayıcısı toocreate ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="91400-173">If you want tooreach hello load balancer by a DNS name, work with your domain service provider toocreate a DNS name for hello rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="91400-174">HTTP veya HTTPS trafiği</span><span class="sxs-lookup"><span data-stu-id="91400-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="91400-175">tooload Bakiye HTTP veya HTTPS trafiği toocontainer web uygulamaları ve Aktarım Katmanı Güvenliği (TLS) için sertifikaları yönetme, hello Kubernetes kullanabileceğiniz [giriş](https://kubernetes.io/docs/user-guide/ingress/) kaynak.</span><span class="sxs-lookup"><span data-stu-id="91400-175">tooload balance HTTP or HTTPS traffic toocontainer web apps and manage certificates for transport layer security (TLS), you can use hello Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="91400-176">Bir giriş tooreach hello küme hizmetlerini gelen bağlantılara izin veren kuralları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="91400-176">An Ingress is a collection of rules that allow inbound connections tooreach hello cluster services.</span></span> <span data-ttu-id="91400-177">Bir giriş kaynak toowork hello Kubernetes küme olmalıdır bir [giriş denetleyicisi](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="91400-177">For an Ingress resource toowork, hello Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="91400-178">Azure kapsayıcı hizmeti Kubernetes giriş denetleyicisi otomatik olarak uygulamıyor.</span><span class="sxs-lookup"><span data-stu-id="91400-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="91400-179">Çeşitli denetleyicisi uygulamalarını kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="91400-179">Several controller implementations are available.</span></span> <span data-ttu-id="91400-180">Şu anda hello [Nginx giriş denetleyicisi](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) tooconfigure giriş kuralları ve HTTP ve HTTPS trafiğinin Yük Dengeleme önerilir.</span><span class="sxs-lookup"><span data-stu-id="91400-180">Currently, hello [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended tooconfigure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="91400-181">Daha fazla bilgi için bkz: Merhaba [Nginx giriş denetleyici belgeleri](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="91400-181">For more information, see hello [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91400-182">Merhaba Nginx giriş denetleyicisi Azure kapsayıcı Hizmeti'nde kullanırken, hello denetleyicisi dağıtımı ile bir hizmet olarak kullanıma `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="91400-182">When using hello Nginx Ingress controller in Azure Container Service, you must expose hello controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="91400-183">Bu, hello Azure yük dengeleyici tooroute trafiği toohello denetleyicisi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="91400-183">This configures hello Azure load balancer tooroute traffic toohello controller.</span></span> <span data-ttu-id="91400-184">Daha fazla bilgi için hello önceki bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="91400-184">For more information, see hello previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="91400-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91400-185">Next steps</span></span>

* <span data-ttu-id="91400-186">Merhaba bkz [Kubernetes LoadBalancer belgeleri](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="91400-186">See hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="91400-187">Daha fazla bilgi edinmek [Kubernetes giriş ve giriş denetleyicileri](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="91400-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="91400-188">Bkz: [Kubernetes örnekleri](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="91400-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

