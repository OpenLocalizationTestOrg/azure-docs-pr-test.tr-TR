---
title: "aaaManage Azure DC/OS kümesi Marathon REST API'si ile | Microsoft Docs"
description: "Kapsayıcıları tooan Azure kapsayıcı hizmeti DC/OS kümesi hello Marathon REST API kullanarak dağıtın."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Kapsayıcılar, Mikro hizmetler, Mesos, Azure"
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a><span data-ttu-id="23742-104">DC/OS hello Marathon REST API'si aracılığıyla kapsayıcı Yönetimi</span><span class="sxs-lookup"><span data-stu-id="23742-104">DC/OS container management through hello Marathon REST API</span></span>
<span data-ttu-id="23742-105">DC/OS dağıtma ve hello temel donanımı özetlerken, kümelenmiş iş yükleri ölçekleme için bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="23742-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="23742-106">DC/OS’nin en üstünde, hesaplama iş yüklerini zamanlamayı ve yürütmeyi yöneten bir çerçeve vardır.</span><span class="sxs-lookup"><span data-stu-id="23742-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="23742-107">Çerçeveler çok sayıda yaygın iş yükü için kullanılabilir, ancak bu belgenin oluşturma ve kapsayıcı dağıtımlarını hello Marathon REST API kullanarak ölçeklendirme başlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="23742-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using hello Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="23742-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="23742-108">Prerequisites</span></span>

<span data-ttu-id="23742-109">Bu örneklerin üzerinden geçmeden önce, Azure Kapsayıcı Hizmeti’nde yapılandırılan bir DC/OS kümeniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="23742-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="23742-110">Ayrıca toohave uzak bağlantı toothis küme gerekir.</span><span class="sxs-lookup"><span data-stu-id="23742-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="23742-111">Bu öğeler hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="23742-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="23742-112">Azure Container Service kümesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="23742-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="23742-113">Tooan Azure kapsayıcı hizmeti kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="23742-113">Connecting tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a><span data-ttu-id="23742-114">Erişim hello DC/OS API'leri</span><span class="sxs-lookup"><span data-stu-id="23742-114">Access hello DC/OS APIs</span></span>
<span data-ttu-id="23742-115">Bağlı toohello Azure kapsayıcı hizmeti kümesi sonra hello DC/OS ve ilgili REST API'lerine http://localhost: Local-port aracılığıyla erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23742-115">After you are connected toohello Azure Container Service cluster, you can access hello DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="23742-116">Bu belgedeki Hello örneklerde, bağlantı noktası 80 üzerinde tünel varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="23742-116">hello examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="23742-117">Örneğin, URI'ler hello Marathon uç noktaları erişilebildiğini itibaren `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="23742-117">For example, hello Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="23742-118">Çeşitli API'ler hello hakkında daha fazla bilgi için hello hello Mesosphere belgelerine bakın [Marathon API'si](https://mesosphere.github.io/marathon/docs/rest-api.html) ve [Chronos API'si](https://mesos.github.io/chronos/docs/api.html)ve hello için Apache belgelerine [Mesos Scheduler API'si ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="23742-118">For more information on hello various APIs, see hello Mesosphere documentation for hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for hello [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="23742-119">DC/OS’den ve Marathon’dan bilgi toplama</span><span class="sxs-lookup"><span data-stu-id="23742-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="23742-120">Toohello DC/OS kümesine kapsayıcıları dağıtmadan önce hello adları ve hello DC/OS aracıların durumu gibi hello DC/OS kümesi hakkında bazı bilgileri toplayın.</span><span class="sxs-lookup"><span data-stu-id="23742-120">Before you deploy containers toohello DC/OS cluster, gather some information about hello DC/OS cluster, such as hello names and status of hello DC/OS agents.</span></span> <span data-ttu-id="23742-121">Bu nedenle, sorgu hello toodo `master/slaves` hello DC/OS REST API uç noktası.</span><span class="sxs-lookup"><span data-stu-id="23742-121">toodo so, query hello `master/slaves` endpoint of hello DC/OS REST API.</span></span> <span data-ttu-id="23742-122">Her şey yolunda giderse hello sorgu her biri için DC/OS aracıları ve çeşitli özellikler listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="23742-122">If everything goes well, hello query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="23742-123">Şimdi hello Marathon kullanın `/apps` geçerli uygulama dağıtımlarını toohello DC/OS kümesi için uç nokta toocheck.</span><span class="sxs-lookup"><span data-stu-id="23742-123">Now, use hello Marathon `/apps` endpoint toocheck for current application deployments toohello DC/OS cluster.</span></span> <span data-ttu-id="23742-124">Bu yeni bir küme ise, uygulamalar için boş bir dizi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="23742-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="23742-125">Docker biçimli kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="23742-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="23742-126">Docker biçimli kapsayıcıları hello Marathon REST API aracılığıyla hello hedeflenen dağıtımı açıklayan bir JSON dosyası kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="23742-126">You deploy Docker-formatted containers through hello Marathon REST API by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="23742-127">Merhaba aşağıdaki örnek Nginx bir kapsayıcı tooa özel aracı hello kümedeki dağıtır.</span><span class="sxs-lookup"><span data-stu-id="23742-127">hello following sample deploys an Nginx container tooa private agent in hello cluster.</span></span> 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="23742-128">toodeploy Docker biçimli bir kapsayıcıyı hello JSON dosyası erişilebilecek bir konuma depolayın.</span><span class="sxs-lookup"><span data-stu-id="23742-128">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="23742-129">Komutu aşağıdaki hello çalıştırmak İleri toodeploy hello kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="23742-129">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="23742-130">Merhaba hello JSON dosyasının adını belirtin (`marathon.json` Bu örnekte).</span><span class="sxs-lookup"><span data-stu-id="23742-130">Specify hello name of hello JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="23742-131">Merhaba çıkış benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="23742-131">hello output is similar toohello following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="23742-132">Şimdi, uygulamalar için marathon'u, bu yeni uygulama hello çıkışında görünür.</span><span class="sxs-lookup"><span data-stu-id="23742-132">Now, if you query Marathon for applications, this new application appears in hello output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a><span data-ttu-id="23742-133">Merhaba kapsayıcı ulaşmak</span><span class="sxs-lookup"><span data-stu-id="23742-133">Reach hello container</span></span>

<span data-ttu-id="23742-134">Nginx bir kapsayıcıda hello özel aracıları hello kümedeki birini çalıştıran bu hello doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23742-134">You can verify that hello Nginx is running in a container on one of hello private agents in hello cluster.</span></span> <span data-ttu-id="23742-135">toofind hello ana bilgisayarı ve bağlantı noktası hello kapsayıcı çalıştığı çalışan görevlerin hello için Marathon sorgu:</span><span class="sxs-lookup"><span data-stu-id="23742-135">toofind hello host and port where hello container is running, query Marathon for hello running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="23742-136">Merhaba değerini bulur `host` hello çıktısında (bir IP adresi benzer çok`10.32.0.x`) ve hello değerini `ports`.</span><span class="sxs-lookup"><span data-stu-id="23742-136">Find hello value of `host` in hello output (an IP address similar too`10.32.0.x`), and hello value of `ports`.</span></span>


<span data-ttu-id="23742-137">Artık bir SSH terminal bağlantısı (tünel bağlantısı değil) toohello yönetim FQDN hello kümesinin olun.</span><span class="sxs-lookup"><span data-stu-id="23742-137">Now make an SSH terminal connection (not a tunneled connection) toohello management FQDN of hello cluster.</span></span> <span data-ttu-id="23742-138">Bağlantı kurulduktan sonra istek aşağıdaki, hello doğru değerini değiştirerek hello olun `host` ve `ports`:</span><span class="sxs-lookup"><span data-stu-id="23742-138">Once connected, make hello following request, substituting hello correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="23742-139">Merhaba Nginx server çıktısı benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="23742-139">hello Nginx server output is similar toohello following:</span></span>

![Kapsayıcısından Nginx](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="23742-141">Kapsayıcılarınızı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="23742-141">Scale your containers</span></span>
<span data-ttu-id="23742-142">Uygulama dağıtımlarını hello Marathon API'si tooscale çıkışı veya ölçek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23742-142">You can use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="23742-143">Merhaba önceki örnekte, uygulamanın bir örneği dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="23742-143">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="23742-144">Şimdi bu uygulamanın toothree örneklerini çıkışı ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="23742-144">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="23742-145">toodo bu nedenle, JSON metnini aşağıdaki hello kullanarak bir JSON dosyası oluşturun ve erişilebilir bir yerde saklayın.</span><span class="sxs-lookup"><span data-stu-id="23742-145">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="23742-146">Tünel bağlantısından hello uygulama çıkış komut tooscale aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="23742-146">From your tunneled connection, run hello following command tooscale out hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="23742-147">Hello URI, http://localhost/marathon/v2/apps/ hello uygulama tooscale hello Kimliğine göre ve ardından ' dir.</span><span class="sxs-lookup"><span data-stu-id="23742-147">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="23742-148">Burada sağlanan hello Nginx örneğini kullanıyorsanız, hello URI http://localhost/marathon/v2/apps/nginx olacaktır.</span><span class="sxs-lookup"><span data-stu-id="23742-148">If you are using hello Nginx sample that is provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="23742-149">Son olarak, uygulamalar için hello Marathon uç noktaya sorgu.</span><span class="sxs-lookup"><span data-stu-id="23742-149">Finally, query hello Marathon endpoint for applications.</span></span> <span data-ttu-id="23742-150">Artık üç adet Nginx kapsayıcısı olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="23742-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="23742-151">Eşdeğer PowerShell komutları</span><span class="sxs-lookup"><span data-stu-id="23742-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="23742-152">Bir Windows sisteminde PowerShell komutlarını kullanarak aynı eylemleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23742-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="23742-153">Aracı adları ve aracı durumu gibi hello DC/OS kümesi hakkında bilgi toogather hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="23742-153">toogather information about hello DC/OS cluster, such as agent names and agent status, run hello following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="23742-154">Docker biçimli kapsayıcıları Marathon aracılığıyla hello hedeflenen dağıtımı açıklayan bir JSON dosyası kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="23742-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="23742-155">Merhaba aşağıdaki örnek hello kapsayıcısının hello DC/OS Aracısı tooport 80 bağlantı noktası 80 bağlama hello Nginx kapsayıcısı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="23742-155">hello following sample deploys hello Nginx container, binding port 80 of hello DC/OS agent tooport 80 of hello container.</span></span>

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="23742-156">toodeploy Docker biçimli bir kapsayıcıyı hello JSON dosyası erişilebilecek bir konuma depolayın.</span><span class="sxs-lookup"><span data-stu-id="23742-156">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="23742-157">Komutu aşağıdaki hello çalıştırmak İleri toodeploy hello kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="23742-157">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="23742-158">Merhaba yolu toohello JSON dosyasını belirtin (`marathon.json` Bu örnekte).</span><span class="sxs-lookup"><span data-stu-id="23742-158">Specify hello path toohello JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="23742-159">Uygulama dağıtımlarını hello Marathon API'si tooscale çıkışı veya ölçek de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23742-159">You can also use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="23742-160">Merhaba önceki örnekte, uygulamanın bir örneği dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="23742-160">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="23742-161">Şimdi bu uygulamanın toothree örneklerini çıkışı ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="23742-161">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="23742-162">toodo bu nedenle, JSON metnini aşağıdaki hello kullanarak bir JSON dosyası oluşturun ve erişilebilir bir yerde saklayın.</span><span class="sxs-lookup"><span data-stu-id="23742-162">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="23742-163">Merhaba uygulama çıkış komut tooscale aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="23742-163">Run hello following command tooscale out hello application:</span></span>

> [!NOTE]
> <span data-ttu-id="23742-164">Hello URI, http://localhost/marathon/v2/apps/ hello uygulama tooscale hello Kimliğine göre ve ardından ' dir.</span><span class="sxs-lookup"><span data-stu-id="23742-164">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="23742-165">Burada sağlanan hello Nginx örneğini kullanıyorsanız, hello URI http://localhost/marathon/v2/apps/nginx olacaktır.</span><span class="sxs-lookup"><span data-stu-id="23742-165">If you are using hello Nginx sample provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="23742-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="23742-166">Next steps</span></span>
* [<span data-ttu-id="23742-167">Merhaba Mesos HTTP uç noktaları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="23742-167">Read more about hello Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="23742-168">Merhaba Marathon REST API'si hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="23742-168">Read more about hello Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

