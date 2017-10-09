---
title: "Azure DC/OS kümesi aaaLoad Bakiye kapsayıcılarında | Microsoft Docs"
description: "Bir Azure kapsayıcı hizmeti DC/OS kümesinde birden çok kapsayıcı arasında Yük Dengelemesi."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, Mikro hizmetler, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="52003-104">Bir Azure kapsayıcı hizmeti DC/OS kümesi Yük Dengelemesi kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="52003-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="52003-105">Bu makalede, Marathon-LB kullanarak Azure kapsayıcı hizmeti DC/OS bir iç yük dengeleyicisi toocreate nasıl yönetileceğini keşfedin.</span><span class="sxs-lookup"><span data-stu-id="52003-105">In this article, we explore how toocreate an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="52003-106">Bu yapılandırma, tooscale yatay uygulamalarınızı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="52003-106">This configuration enables you tooscale your applications horizontally.</span></span> <span data-ttu-id="52003-107">Ayrıca, hello ortak ve özel aracı kümeleri tootake avantajlarından hello ortak küme ve uygulama kapsayıcılarınızı hello özel kümede yük dengeleyici koyarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="52003-107">It also allows you tootake advantage of hello public and private agent clusters by placing your load balancers on hello public cluster and your application containers on hello private cluster.</span></span> <span data-ttu-id="52003-108">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="52003-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52003-109">Marathon yük dengeleyici yapılandırma</span><span class="sxs-lookup"><span data-stu-id="52003-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="52003-110">Merhaba yük dengeleyici kullanarak bir uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="52003-110">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="52003-111">Yapılandırma ve Azure yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="52003-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="52003-112">Bir ACS DC/küme toocomplete hello bu öğreticideki adımlar işletim sistemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="52003-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="52003-113">Gerekirse, [bu komut dosyası örneği](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) sizin için bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52003-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="52003-114">Bu öğretici hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="52003-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="52003-115">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="52003-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="52003-116">Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="52003-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="52003-117">Yükü Dengeleme'ye genel bakış</span><span class="sxs-lookup"><span data-stu-id="52003-117">Load balancing overview</span></span>

<span data-ttu-id="52003-118">Bir Azure kapsayıcı hizmeti DC/OS kümesinde iki yük dengeleyici katmanı vardır:</span><span class="sxs-lookup"><span data-stu-id="52003-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="52003-119">**Azure yük dengeleyici** ortak giriş noktaları (olanları, son kullanıcıların erişim hello) sağlar.</span><span class="sxs-lookup"><span data-stu-id="52003-119">**Azure Load Balancer** provides public entry points (hello ones that end users access).</span></span> <span data-ttu-id="52003-120">Bir Azure LB otomatik olarak Azure kapsayıcı hizmeti tarafından sağlanır ve, varsayılan olarak, yapılandırılmış tooexpose bağlantı noktası 80, 443 ve 8080.</span><span class="sxs-lookup"><span data-stu-id="52003-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured tooexpose port 80, 443 and 8080.</span></span>

<span data-ttu-id="52003-121">**Merhaba Marathon yük dengeleyici (marathon-lb)** yollar gelen istekleri servis istekleri toocontainer örnekleri.</span><span class="sxs-lookup"><span data-stu-id="52003-121">**hello Marathon Load Balancer (marathon-lb)** routes inbound requests toocontainer instances that service these requests.</span></span> <span data-ttu-id="52003-122">Biz bizim web hizmeti sağlayan hello kapsayıcıları ölçeklendirirken hello marathon-lb dinamik olarak uyum sağlar.</span><span class="sxs-lookup"><span data-stu-id="52003-122">As we scale hello containers providing our web service, hello marathon-lb dynamically adapts.</span></span> <span data-ttu-id="52003-123">Bu yük dengeleyici varsayılan olarak, kapsayıcı hizmeti tarafından sağlanan değil ancak kolay tooinstall işlem.</span><span class="sxs-lookup"><span data-stu-id="52003-123">This load balancer is not provided by default in your Container Service, but it is easy tooinstall.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="52003-124">Marathon yük dengeleyici yapılandırma</span><span class="sxs-lookup"><span data-stu-id="52003-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="52003-125">Marathon yük dengeleyici kendisini dağıttıktan sonra Merhaba kapsayıcılara göre dinamik olarak yeniden yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="52003-125">Marathon Load Balancer dynamically reconfigures itself based on hello containers that you've deployed.</span></span> <span data-ttu-id="52003-126">Bu olursa, Apache Mesos başka yerde hello kapsayıcıyı yeniden başlatır ve marathon-lb uyum de kapsayıcı ya da bir aracı - esnek toohello kaybı olabilir.</span><span class="sxs-lookup"><span data-stu-id="52003-126">It's also resilient toohello loss of a container or an agent - if this occurs, Apache Mesos restarts hello container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="52003-127">Çalışma hello aşağıdaki tooinstall hello marathon yük dengeleyici hello ortak aracısının kümede komutu.</span><span class="sxs-lookup"><span data-stu-id="52003-127">Run hello following command tooinstall hello marathon load balancer on hello public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="52003-128">Yük dengeli uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="52003-128">Deploy load balanced application</span></span>

<span data-ttu-id="52003-129">Biz hello marathon-lb paketine sahip olduğunuza göre biz tooload Bakiye istediğimiz bir uygulama kapsayıcısı dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52003-129">Now that we have hello marathon-lb package, we can deploy an application container that we wish tooload balance.</span></span> 

<span data-ttu-id="52003-130">İlk olarak, hello genel olarak kullanıma sunulan hello aracıları FQDN'sini alın.</span><span class="sxs-lookup"><span data-stu-id="52003-130">First, get hello FQDN of hello publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="52003-131">Ardından, adlı bir dosya oluşturun *hello web.json* ve hello kopyasında aşağıdaki içeriği.</span><span class="sxs-lookup"><span data-stu-id="52003-131">Next, create a file named *hello-web.json* and copy in hello following contents.</span></span> <span data-ttu-id="52003-132">Merhaba `HAPROXY_0_VHOST` etiket hello hello DC/OS aracıları FQDN'si ile güncelleştirilmiş toobe gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="52003-132">hello `HAPROXY_0_VHOST` label needs toobe updated with hello FQDN of hello DC/OS agents.</span></span> 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

<span data-ttu-id="52003-133">Merhaba DC/OS CLI toorun hello uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="52003-133">Use hello DC/OS CLI toorun hello application.</span></span> <span data-ttu-id="52003-134">Varsayılan olarak Marathon hello hello uygulama toohello özel küme dağıtır.</span><span class="sxs-lookup"><span data-stu-id="52003-134">By default Marathon deploys hello hello applicaton toohello private cluster.</span></span> <span data-ttu-id="52003-135">Dağıtım hello Bunun anlamı yalnızca, genellikle istenen hello davranış olduğu, yük dengeleyici erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="52003-135">This means that hello above deployment is only accessible via your load balancer, which is usually hello desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="52003-136">Merhaba uygulama dağıtıldıktan sonra toohello Merhaba Aracısı küme tooview yükü dengelenmiş uygulaması'nın FQDN'si göz atın.</span><span class="sxs-lookup"><span data-stu-id="52003-136">Once hello application has been deployed, browse toohello FQDN of hello agent cluster tooview load balanced application.</span></span>

![Yük dengeli uygulama görüntüsü](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="52003-138">Azure yük dengeleyici yapılandırma</span><span class="sxs-lookup"><span data-stu-id="52003-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="52003-139">Varsayılan olarak, Azure Load Balancer 80, 8080 ve 443 bağlantı noktalarını ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="52003-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="52003-140">Kullanıyorsanız (Yukarıdaki örnek hello içinde yaptığımız) üç bağlantı noktaları ardından toodo gereken bir şey yok.</span><span class="sxs-lookup"><span data-stu-id="52003-140">If you're using one of these three ports (as we do in hello above example), then there is nothing you need toodo.</span></span> <span data-ttu-id="52003-141">Mümkün toohit olmalıdır, aracı yük dengeleyicinin FQDN ve her yenilediğinizde, üç web sunucusundan bir hepsini şekilde birini isabet.</span><span class="sxs-lookup"><span data-stu-id="52003-141">You should be able toohit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="52003-142">Tooadd bir hepsini bir kez deneme kuralı ve bir araştırma hello yük dengeleyici üzerinde farklı bir bağlantı noktası kullanıyorsanız, kullandığınız hello için bağlantı noktası gerekir.</span><span class="sxs-lookup"><span data-stu-id="52003-142">If you use a different port, you need tooadd a round-robin rule and a probe on hello load balancer for hello port that you used.</span></span> <span data-ttu-id="52003-143">Hello bunu yapabilirsiniz [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), hello komutlarla `azure network lb rule create` ve `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="52003-143">You can do this from hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with hello commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52003-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="52003-144">Next steps</span></span>

<span data-ttu-id="52003-145">Bu öğreticide, yük dengelemeyi hello Marathon hem Azure yük dengeleyicileri dahil olmak üzere aşağıdaki eylemler hello ACS hakkında öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="52003-145">In this tutorial, you learned about load balancing in ACS with both hello Marathon and Azure load balancers including hello following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52003-146">Marathon yük dengeleyici yapılandırma</span><span class="sxs-lookup"><span data-stu-id="52003-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="52003-147">Merhaba yük dengeleyici kullanarak bir uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="52003-147">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="52003-148">Yapılandırma ve Azure yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="52003-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="52003-149">Azure depolama DC/OS Azure ile tümleştirme hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="52003-149">Advance toohello next tutorial toolearn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52003-150">DC/OS kümesi bağlama Azure dosya paylaşımı</span><span class="sxs-lookup"><span data-stu-id="52003-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)