---
title: "Azure DC/OS kümesi Marathon REST API ile yönetme | Microsoft Docs"
description: "Marathon REST API kullanarak Azure kapsayıcı hizmeti DC/OS kümesine kapsayıcıları dağıtın."
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
ms.openlocfilehash: 65f8e0170fa7b89162e811a1d5dd58775fd20d7b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-container-management-through-the-marathon-rest-api"></a><span data-ttu-id="84095-104">DC/OS Marathon REST API'si aracılığıyla kapsayıcı Yönetimi</span><span class="sxs-lookup"><span data-stu-id="84095-104">DC/OS container management through the Marathon REST API</span></span>
<span data-ttu-id="84095-105">DC/OS, temel donanımı özetlerken, kümelenmiş iş yüklerini dağıtmak ve ölçeklendirmek için ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="84095-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="84095-106">DC/OS’nin en üstünde, hesaplama iş yüklerini zamanlamayı ve yürütmeyi yöneten bir çerçeve vardır.</span><span class="sxs-lookup"><span data-stu-id="84095-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="84095-107">Çerçeveler çok sayıda yaygın iş yükü için kullanılabilir, ancak bu belgenin oluşturma ve Marathon REST API'sini kullanarak kapsayıcı dağıtımlarını ölçeklendirme başlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="84095-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using the Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="84095-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="84095-108">Prerequisites</span></span>

<span data-ttu-id="84095-109">Bu örneklerin üzerinden geçmeden önce, Azure Kapsayıcı Hizmeti’nde yapılandırılan bir DC/OS kümeniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="84095-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="84095-110">Bu kümeye uzaktan bağlantınız olması da gerekir.</span><span class="sxs-lookup"><span data-stu-id="84095-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="84095-111">Bu öğeler hakkında daha fazla bilgi için, aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="84095-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="84095-112">Azure Container Service kümesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="84095-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="84095-113">Azure Container Service kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="84095-113">Connecting to an Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-the-dcos-apis"></a><span data-ttu-id="84095-114">DC/OS API'lere erişim</span><span class="sxs-lookup"><span data-stu-id="84095-114">Access the DC/OS APIs</span></span>
<span data-ttu-id="84095-115">Azure Kapsayıcı Hizmeti kümesine bağlandıktan sonra, DC/OS’ye ve ilgili REST API’lerine http://localhost:local-port aracılığıyla erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84095-115">After you are connected to the Azure Container Service cluster, you can access the DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="84095-116">Bu belgedeki örneklerde, bağlantı noktası 80 üzerinde tünel oluşturulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="84095-116">The examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="84095-117">Örneğin, Marathon uç noktaları URI'ler erişilebildiğini itibaren `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="84095-117">For example, the Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="84095-118">Çeşitli API'ler hakkında daha fazla bilgi için, [Marathon API’si](https://mesosphere.github.io/marathon/docs/rest-api.html) ve [Chronos API’si](https://mesos.github.io/chronos/docs/api.html) için Mesosphere belgelerine ve [Mesos Scheduler API’si](http://mesos.apache.org/documentation/latest/scheduler-http-api/) için Apache belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="84095-118">For more information on the various APIs, see the Mesosphere documentation for the [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for the [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="84095-119">DC/OS’den ve Marathon’dan bilgi toplama</span><span class="sxs-lookup"><span data-stu-id="84095-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="84095-120">DC/OS kümesine kapsayıcıları dağıtmadan önce adları ve DC/OS aracıların durumu gibi DC/OS kümesi hakkında bazı bilgileri toplayın.</span><span class="sxs-lookup"><span data-stu-id="84095-120">Before you deploy containers to the DC/OS cluster, gather some information about the DC/OS cluster, such as the names and status of the DC/OS agents.</span></span> <span data-ttu-id="84095-121">Bunu yapmak için, DC/OS REST API’sinin `master/slaves` uç noktasını sorgulayın. </span><span class="sxs-lookup"><span data-stu-id="84095-121">To do so, query the `master/slaves` endpoint of the DC/OS REST API.</span></span> <span data-ttu-id="84095-122">Her şey yolunda giderse, sorgu DC/OS aracıları ve her biri için çeşitli özellikler listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="84095-122">If everything goes well, the query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="84095-123">Şimdi, DC/OS kümesine geçerli uygulama dağıtımlarını denetlemek için Marathon `/apps` uç noktasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="84095-123">Now, use the Marathon `/apps` endpoint to check for current application deployments to the DC/OS cluster.</span></span> <span data-ttu-id="84095-124">Bu yeni bir küme ise, uygulamalar için boş bir dizi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="84095-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="84095-125">Docker biçimli kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="84095-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="84095-126">Docker biçimli kapsayıcıları Marathon REST API'si aracılığıyla hedeflenen dağıtımı açıklayan bir JSON dosyası kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="84095-126">You deploy Docker-formatted containers through the Marathon REST API by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="84095-127">Aşağıdaki örnek bir Nginx kapsayıcısı kümedeki özel bir aracıya dağıtır.</span><span class="sxs-lookup"><span data-stu-id="84095-127">The following sample deploys an Nginx container to a private agent in the cluster.</span></span> 

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

<span data-ttu-id="84095-128">Docker biçimli bir kapsayıcıyı dağıtmak için JSON dosyasının erişilebilir bir yerde saklayın.</span><span class="sxs-lookup"><span data-stu-id="84095-128">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="84095-129">Ardından, kapsayıcıyı dağıtmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="84095-129">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="84095-130">JSON dosyasının adını belirtin (`marathon.json` Bu örnekte).</span><span class="sxs-lookup"><span data-stu-id="84095-130">Specify the name of the JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="84095-131">Çıkış aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="84095-131">The output is similar to the following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="84095-132">Şimdi, uygulamalar için Marathon’u sorguladığınızda, bu yeni uygulama çıktıda görünür.</span><span class="sxs-lookup"><span data-stu-id="84095-132">Now, if you query Marathon for applications, this new application appears in the output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-the-container"></a><span data-ttu-id="84095-133">Kapsayıcı ulaşmak</span><span class="sxs-lookup"><span data-stu-id="84095-133">Reach the container</span></span>

<span data-ttu-id="84095-134">Özel aracıları kümedeki birinde Nginx bir kapsayıcıda çalışıp çalışmadığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84095-134">You can verify that the Nginx is running in a container on one of the private agents in the cluster.</span></span> <span data-ttu-id="84095-135">Kapsayıcı çalıştığı bağlantı noktası ve ana bilgisayar bulmak için çalışan görevler için Marathon sorgu:</span><span class="sxs-lookup"><span data-stu-id="84095-135">To find the host and port where the container is running, query Marathon for the running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="84095-136">Değerini bulur `host` çıktıda (benzer şekilde bir IP adresi `10.32.0.x`) ve değeri `ports`.</span><span class="sxs-lookup"><span data-stu-id="84095-136">Find the value of `host` in the output (an IP address similar to `10.32.0.x`), and the value of `ports`.</span></span>


<span data-ttu-id="84095-137">Şimdi küme yönetimi FQDN için bir SSH terminal bağlantısı (tünel bağlantısı değil) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84095-137">Now make an SSH terminal connection (not a tunneled connection) to the management FQDN of the cluster.</span></span> <span data-ttu-id="84095-138">Bağlantı kurulduktan sonra doğru değerini değiştirerek aşağıdaki, istekte `host` ve `ports`:</span><span class="sxs-lookup"><span data-stu-id="84095-138">Once connected, make the following request, substituting the correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="84095-139">Nginx server çıktısı aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="84095-139">The Nginx server output is similar to the following:</span></span>

![Kapsayıcısından Nginx](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="84095-141">Kapsayıcılarınızı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="84095-141">Scale your containers</span></span>
<span data-ttu-id="84095-142">Ölçeği genişletme veya ölçeklendirmek için Marathon API'si kullanabilirsiniz uygulama dağıtımlarda.</span><span class="sxs-lookup"><span data-stu-id="84095-142">You can use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="84095-143">Önceki örnekte, uygulamanın bir örneğini dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="84095-143">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="84095-144">Şimdi bunun ölçeğini uygulamanın üç örneğine genişletelim.</span><span class="sxs-lookup"><span data-stu-id="84095-144">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="84095-145">Bunu yapmak için, aşağıdaki JSON metnini kullanarak bir JSON dosyası oluşturun ve erişilebilir bir konumda depolayın.</span><span class="sxs-lookup"><span data-stu-id="84095-145">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="84095-146">Tünel bağlantısından uygulamanın ölçeğini genişletmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="84095-146">From your tunneled connection, run the following command to scale out the application.</span></span>

> [!NOTE]
> <span data-ttu-id="84095-147">URI, http://localhost/marathon/v2/apps/ şeklinde olur ve ardından ölçeklendirilecek uygulamanın kimliği gelir.</span><span class="sxs-lookup"><span data-stu-id="84095-147">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="84095-148">Burada sağlanan Nginx örneğini kullanıyorsanız, URI http://localhost/marathon/v2/apps/nginx şeklinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="84095-148">If you are using the Nginx sample that is provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="84095-149">Son olarak, uygulamalar için Marathon uç noktasını sorgulayın.</span><span class="sxs-lookup"><span data-stu-id="84095-149">Finally, query the Marathon endpoint for applications.</span></span> <span data-ttu-id="84095-150">Artık üç adet Nginx kapsayıcısı olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="84095-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="84095-151">Eşdeğer PowerShell komutları</span><span class="sxs-lookup"><span data-stu-id="84095-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="84095-152">Bir Windows sisteminde PowerShell komutlarını kullanarak aynı eylemleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84095-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="84095-153">Aracı adları ve aracı durumu gibi DC/OS kümesi hakkında bilgi toplamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="84095-153">To gather information about the DC/OS cluster, such as agent names and agent status, run the following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="84095-154">Docker biçimli kapsayıcıları Marathon aracılığıyla, hedeflenen dağıtımı açıklayan bir JSON dosyası kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="84095-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="84095-155">Aşağıdaki örnek, Nginx kapsayıcısı DC/OS aracısı bağlama bağlantı noktası 80'i kapsayıcının 80 numaralı bağlantı noktasına dağıtır.</span><span class="sxs-lookup"><span data-stu-id="84095-155">The following sample deploys the Nginx container, binding port 80 of the DC/OS agent to port 80 of the container.</span></span>

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

<span data-ttu-id="84095-156">Docker biçimli bir kapsayıcıyı dağıtmak için JSON dosyasının erişilebilir bir yerde saklayın.</span><span class="sxs-lookup"><span data-stu-id="84095-156">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="84095-157">Ardından, kapsayıcıyı dağıtmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="84095-157">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="84095-158">JSON dosyasının yolunu belirtin (`marathon.json` Bu örnekte).</span><span class="sxs-lookup"><span data-stu-id="84095-158">Specify the path to the JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="84095-159">Marathon API’sini uygulama dağıtımlarının ölçeğini genişletmek ve ölçeğini daraltmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84095-159">You can also use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="84095-160">Önceki örnekte, uygulamanın bir örneğini dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="84095-160">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="84095-161">Şimdi bunun ölçeğini uygulamanın üç örneğine genişletelim.</span><span class="sxs-lookup"><span data-stu-id="84095-161">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="84095-162">Bunu yapmak için, aşağıdaki JSON metnini kullanarak bir JSON dosyası oluşturun ve erişilebilir bir konumda depolayın.</span><span class="sxs-lookup"><span data-stu-id="84095-162">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="84095-163">Uygulamanın ölçeğini genişletmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="84095-163">Run the following command to scale out the application:</span></span>

> [!NOTE]
> <span data-ttu-id="84095-164">URI, http://localhost/marathon/v2/apps/ şeklinde olur ve ardından ölçeklendirilecek uygulamanın kimliği gelir.</span><span class="sxs-lookup"><span data-stu-id="84095-164">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="84095-165">Burada sağlanan Nginx örneğini kullanıyorsanız, URI http://localhost/marathon/v2/apps/nginx şeklinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="84095-165">If you are using the Nginx sample provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="84095-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="84095-166">Next steps</span></span>
* [<span data-ttu-id="84095-167">Mesos HTTP uç noktaları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="84095-167">Read more about the Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="84095-168">Marathon REST API'si hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="84095-168">Read more about the Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

