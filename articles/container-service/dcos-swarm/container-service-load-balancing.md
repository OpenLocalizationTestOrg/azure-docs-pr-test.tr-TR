---
title: "Azure DC/OS kümesi Bakiye kapsayıcılarında yük | Microsoft Docs"
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
ms.openlocfilehash: 78725c9d23e13d307821a188028ef573d1def038
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="3caf9-104">Bir Azure kapsayıcı hizmeti DC/OS kümesi Yük Dengelemesi kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="3caf9-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="3caf9-105">Bu makalede, Marathon-LB kullanarak bir DC/OS yönetilen Azure kapsayıcı Hizmeti'nde bir iç yük dengeleyici oluşturma keşfedin.</span><span class="sxs-lookup"><span data-stu-id="3caf9-105">In this article, we explore how to create an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="3caf9-106">Bu yapılandırma, uygulamalarınızı yatay ölçek sağlar.</span><span class="sxs-lookup"><span data-stu-id="3caf9-106">This configuration enables you to scale your applications horizontally.</span></span> <span data-ttu-id="3caf9-107">Ayrıca, ortak ve özel aracı kümeleri ortak küme ve uygulama kapsayıcılarınızı özel kümede yük dengeleyici koyarak yararlanmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3caf9-107">It also allows you to take advantage of the public and private agent clusters by placing your load balancers on the public cluster and your application containers on the private cluster.</span></span> <span data-ttu-id="3caf9-108">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="3caf9-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3caf9-109">Marathon yük dengeleyici yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3caf9-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="3caf9-110">Yük Dengeleyici kullanarak bir uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="3caf9-110">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="3caf9-111">Yapılandırma ve Azure yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="3caf9-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="3caf9-112">Bu öğreticide adımları tamamlamak için bir ACS DC/OS kümesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3caf9-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="3caf9-113">Gerekirse, [bu komut dosyası örneği](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) sizin için bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3caf9-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="3caf9-114">Bu öğretici, Azure CLI 2.0.4 veya sonraki bir sürümü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3caf9-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3caf9-115">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3caf9-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="3caf9-116">Yükseltme gerekiyorsa, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3caf9-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="3caf9-117">Yükü Dengeleme'ye genel bakış</span><span class="sxs-lookup"><span data-stu-id="3caf9-117">Load balancing overview</span></span>

<span data-ttu-id="3caf9-118">Bir Azure kapsayıcı hizmeti DC/OS kümesinde iki yük dengeleyici katmanı vardır:</span><span class="sxs-lookup"><span data-stu-id="3caf9-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="3caf9-119">**Azure yük dengeleyici** ortak giriş noktaları (son kullanıcıların erişim olanlar) sağlar.</span><span class="sxs-lookup"><span data-stu-id="3caf9-119">**Azure Load Balancer** provides public entry points (the ones that end users access).</span></span> <span data-ttu-id="3caf9-120">Bir Azure LB Azure kapsayıcı hizmeti tarafından otomatik olarak sağlanır ve, bağlantı noktası 80, 443 ve 8080 kullanıma sunmak için yapılandırılmış varsayılan olarak açıktır.</span><span class="sxs-lookup"><span data-stu-id="3caf9-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured to expose port 80, 443 and 8080.</span></span>

<span data-ttu-id="3caf9-121">**Marathon yük dengeleyici (marathon-lb)** yollar gelen istekleri bu istekleri kapsayıcı örnekleri.</span><span class="sxs-lookup"><span data-stu-id="3caf9-121">**The Marathon Load Balancer (marathon-lb)** routes inbound requests to container instances that service these requests.</span></span> <span data-ttu-id="3caf9-122">Biz bizim web hizmet sağlayan kapsayıcıları ölçeklendirirken marathon-lb dinamik olarak uyum sağlar.</span><span class="sxs-lookup"><span data-stu-id="3caf9-122">As we scale the containers providing our web service, the marathon-lb dynamically adapts.</span></span> <span data-ttu-id="3caf9-123">Bu yük dengeleyici varsayılan olarak, kapsayıcı hizmeti tarafından sağlanan değil, ancak yüklemek kolaydır.</span><span class="sxs-lookup"><span data-stu-id="3caf9-123">This load balancer is not provided by default in your Container Service, but it is easy to install.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="3caf9-124">Marathon yük dengeleyici yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3caf9-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="3caf9-125">Marathon Yük Dengeleyici dağıttığınız kapsayıcılara göre kendini dinamik olarak yeniden yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="3caf9-125">Marathon Load Balancer dynamically reconfigures itself based on the containers that you've deployed.</span></span> <span data-ttu-id="3caf9-126">Ayrıca bu olursa, Apache Mesos başka yerde kapsayıcıyı yeniden başlatır ve marathon-lb uyum bir kapsayıcı veya bir aracı - kaybı esnek değildir.</span><span class="sxs-lookup"><span data-stu-id="3caf9-126">It's also resilient to the loss of a container or an agent - if this occurs, Apache Mesos restarts the container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="3caf9-127">Marathon yük dengeleyici genel aracısının kümede yüklemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3caf9-127">Run the following command to install the marathon load balancer on the public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="3caf9-128">Yük dengeli uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="3caf9-128">Deploy load balanced application</span></span>

<span data-ttu-id="3caf9-129">Marathon-lb paketine sahip olduğumuza göre yük dengeleme işlemi uygulamak istediğimiz bir uygulama kapsayıcısını dağıtabiliriz.</span><span class="sxs-lookup"><span data-stu-id="3caf9-129">Now that we have the marathon-lb package, we can deploy an application container that we wish to load balance.</span></span> 

<span data-ttu-id="3caf9-130">İlk olarak, genel olarak sunulan aracıları FQDN'sini alın.</span><span class="sxs-lookup"><span data-stu-id="3caf9-130">First, get the FQDN of the publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="3caf9-131">Ardından, adlı bir dosya oluşturun *hello web.json* ve aşağıdaki içeriği kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3caf9-131">Next, create a file named *hello-web.json* and copy in the following contents.</span></span> <span data-ttu-id="3caf9-132">`HAPROXY_0_VHOST` Etiket DC/OS aracıları FQDN ile güncelleştirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="3caf9-132">The `HAPROXY_0_VHOST` label needs to be updated with the FQDN of the DC/OS agents.</span></span> 

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

<span data-ttu-id="3caf9-133">Uygulamayı çalıştırmak için DC/OS CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="3caf9-133">Use the DC/OS CLI to run the application.</span></span> <span data-ttu-id="3caf9-134">Varsayılan olarak Marathon dağıtır özel kümeye uygulama.</span><span class="sxs-lookup"><span data-stu-id="3caf9-134">By default Marathon deploys the the applicaton to the private cluster.</span></span> <span data-ttu-id="3caf9-135">Bu, genellikle istenen davranışı olduğu yukarıdaki dağıtım yalnızca, yük dengeleyici erişilebilir olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3caf9-135">This means that the above deployment is only accessible via your load balancer, which is usually the desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="3caf9-136">Uygulama dağıtıldıktan sonra Yük dengeli uygulama görüntülemek için aracı küme FQDN'si için göz atın.</span><span class="sxs-lookup"><span data-stu-id="3caf9-136">Once the application has been deployed, browse to the FQDN of the agent cluster to view load balanced application.</span></span>

![Yük dengeli uygulama görüntüsü](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="3caf9-138">Azure yük dengeleyici yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3caf9-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="3caf9-139">Varsayılan olarak, Azure Load Balancer 80, 8080 ve 443 bağlantı noktalarını ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="3caf9-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="3caf9-140">Bu bağlantı noktalarından birini kullanıyorsanız (yukarıdaki örnekte olduğu gibi) bir şey yapmanıza gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="3caf9-140">If you're using one of these three ports (as we do in the above example), then there is nothing you need to do.</span></span> <span data-ttu-id="3caf9-141">Aracı yük dengeleyicinin FQDN isabet gerekir ve her yenilediğinizde, üç web sunucusundan bir hepsini şekilde birini isabet.</span><span class="sxs-lookup"><span data-stu-id="3caf9-141">You should be able to hit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="3caf9-142">Farklı bir bağlantı noktası kullanıyorsanız, kullandığınız bağlantı noktası için yük dengeleyicide hepsini bir kez deneme kuralı ve bir araştırma eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3caf9-142">If you use a different port, you need to add a round-robin rule and a probe on the load balancer for the port that you used.</span></span> <span data-ttu-id="3caf9-143">Bunu [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md)’dan `azure network lb rule create` ve `azure network lb probe create` komutlarıyla yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3caf9-143">You can do this from the [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with the commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3caf9-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3caf9-144">Next steps</span></span>

<span data-ttu-id="3caf9-145">Bu öğreticide, aşağıdaki eylemleri de dahil olmak üzere Marathon ve Azure yük dengeleyici ile ACS dengelemesini hakkında öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="3caf9-145">In this tutorial, you learned about load balancing in ACS with both the Marathon and Azure load balancers including the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3caf9-146">Marathon yük dengeleyici yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3caf9-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="3caf9-147">Yük Dengeleyici kullanarak bir uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="3caf9-147">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="3caf9-148">Yapılandırma ve Azure yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="3caf9-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="3caf9-149">Azure depolama DC/OS Azure ile tümleştirme hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="3caf9-149">Advance to the next tutorial to learn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3caf9-150">DC/OS kümesi bağlama Azure dosya paylaşımı</span><span class="sxs-lookup"><span data-stu-id="3caf9-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)