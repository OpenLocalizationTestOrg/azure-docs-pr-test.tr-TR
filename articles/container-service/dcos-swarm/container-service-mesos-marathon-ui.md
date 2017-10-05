---
title: "Azure DC/OS kümesi Marathon kullanıcı Arabirimi ile yönetme | Microsoft Docs"
description: "Marathon web kullanıcı arabirimini kullanarak Azure Kapsayıcı Hizmeti küme hizmetine kapsayıcıları dağıtın."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Kapsayıcılar, Mikro hizmetler, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: b00088bb005519dc5d533433308c0e3e33c7f433
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-the-marathon-web-ui"></a><span data-ttu-id="85a8b-104">Marathon web UI üzerinden bir Azure Container Service DC/OS kümesini yönetme</span><span class="sxs-lookup"><span data-stu-id="85a8b-104">Manage an Azure Container Service DC/OS cluster through the Marathon web UI</span></span>
<span data-ttu-id="85a8b-105">DC/OS, temel donanımı özetlerken, kümelenmiş iş yüklerini dağıtmak ve ölçeklendirmek için ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="85a8b-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="85a8b-106">DC/OS’nin en üstünde, hesaplama iş yüklerini zamanlamayı ve yürütmeyi yöneten bir çerçeve vardır.</span><span class="sxs-lookup"><span data-stu-id="85a8b-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="85a8b-107">Çerçeveler çok sayıda yaygın iş yükü için kullanılabilir, ancak bu belgede Marathon ile kapsayıcı dağıtımına başlamak açıklar.</span><span class="sxs-lookup"><span data-stu-id="85a8b-107">While frameworks are available for many popular workloads, this document describes how to get started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="85a8b-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="85a8b-108">Prerequisites</span></span>
<span data-ttu-id="85a8b-109">Bu örneklerin üzerinden geçmeden önce, Azure Kapsayıcı Hizmeti’nde yapılandırılan bir DC/OS kümeniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="85a8b-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="85a8b-110">Bu kümeye uzaktan bağlantınız olması da gerekir.</span><span class="sxs-lookup"><span data-stu-id="85a8b-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="85a8b-111">Bu öğeler hakkında daha fazla bilgi için, aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="85a8b-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="85a8b-112">Azure Container Service kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="85a8b-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="85a8b-113">Azure Container Service kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="85a8b-113">Connect to an Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="85a8b-114">Bu makalede, yerel bağlantı noktası 80 üzerinden DC/OS kümesine tünel varsayar.</span><span class="sxs-lookup"><span data-stu-id="85a8b-114">This article assumes you are tunneling to the DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-the-dcos-ui"></a><span data-ttu-id="85a8b-115">DC/OS kullanıcı arabirimini keşfetme</span><span class="sxs-lookup"><span data-stu-id="85a8b-115">Explore the DC/OS UI</span></span>
<span data-ttu-id="85a8b-116">Secure Shell (SSH) tüneli [oluşturarak](../container-service-connect.md) http://localhost/ adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="85a8b-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse to http://localhost/.</span></span> <span data-ttu-id="85a8b-117">Bu, DC/OS web kullanıcı arabirimini yükler ve kullanılan kaynaklar, etkin aracılar ve çalışan hizmetler gibi, küme hakkında bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="85a8b-117">This loads the DC/OS web UI and shows information about the cluster, such as used resources, active agents, and running services.</span></span>

![DC/OS Kullanıcı Arabirimi](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-the-marathon-ui"></a><span data-ttu-id="85a8b-119">Marathon kullanıcı arabirimini keşfetme</span><span class="sxs-lookup"><span data-stu-id="85a8b-119">Explore the Marathon UI</span></span>
<span data-ttu-id="85a8b-120">Marathon kullanıcı arabirimini görmek için http://localhost/marathon adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="85a8b-120">To see the Marathon UI, browse to http://localhost/marathon.</span></span> <span data-ttu-id="85a8b-121">Bu ekranda, Azure Kapsayıcı Hizmeti DC/OS kümesinde yeni kapsayıcı veya başka bir uygulama başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85a8b-121">From this screen, you can start a new container or another application on the Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="85a8b-122">Kapsayıcıları ve uygulamaları çalıştırma hakkında bilgileri de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85a8b-122">You can also see information about running containers and applications.</span></span>  

![Marathon kullanıcı arabirimi](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="85a8b-124">Docker biçimli kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="85a8b-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="85a8b-125">Yeni kapsayıcıyı Marathon kullanarak dağıtmak için **Uygulama Oluştur**'a tıklayın ve form sekmelerine aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="85a8b-125">To deploy a new container by using Marathon, click **Create Application**, and enter the following information into the form tabs:</span></span>

| <span data-ttu-id="85a8b-126">Alan</span><span class="sxs-lookup"><span data-stu-id="85a8b-126">Field</span></span> | <span data-ttu-id="85a8b-127">Değer</span><span class="sxs-lookup"><span data-stu-id="85a8b-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="85a8b-128">Kimlik</span><span class="sxs-lookup"><span data-stu-id="85a8b-128">ID</span></span> |<span data-ttu-id="85a8b-129">nginx</span><span class="sxs-lookup"><span data-stu-id="85a8b-129">nginx</span></span> |
| <span data-ttu-id="85a8b-130">Bellek</span><span class="sxs-lookup"><span data-stu-id="85a8b-130">Memory</span></span> | <span data-ttu-id="85a8b-131">32</span><span class="sxs-lookup"><span data-stu-id="85a8b-131">32</span></span> |
| <span data-ttu-id="85a8b-132">Görüntü</span><span class="sxs-lookup"><span data-stu-id="85a8b-132">Image</span></span> |<span data-ttu-id="85a8b-133">nginx</span><span class="sxs-lookup"><span data-stu-id="85a8b-133">nginx</span></span> |
| <span data-ttu-id="85a8b-134">Ağ</span><span class="sxs-lookup"><span data-stu-id="85a8b-134">Network</span></span> |<span data-ttu-id="85a8b-135">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="85a8b-135">Bridged</span></span> |
| <span data-ttu-id="85a8b-136">Ana Bilgisayar Bağlantı Noktası</span><span class="sxs-lookup"><span data-stu-id="85a8b-136">Host Port</span></span> |<span data-ttu-id="85a8b-137">80</span><span class="sxs-lookup"><span data-stu-id="85a8b-137">80</span></span> |
| <span data-ttu-id="85a8b-138">Protokol</span><span class="sxs-lookup"><span data-stu-id="85a8b-138">Protocol</span></span> |<span data-ttu-id="85a8b-139">TCP</span><span class="sxs-lookup"><span data-stu-id="85a8b-139">TCP</span></span> |

![Yeni Uygulama Kullanıcı Arabirimi --Genel](./media/container-service-mesos-marathon-ui/dcos4.png)

![Yeni Uygulama Kullanıcı Arabirimi--Docker Kapsayıcısı](./media/container-service-mesos-marathon-ui/dcos5.png)

![Yeni Uygulama Kullanıcı Arabirimi--Bağlantı Noktaları ve Hizmet Bulma](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="85a8b-143">Kapsayıcı bağlantı noktasını statik olarak aracıdaki bağlantı noktasıyla eşlemek istiyorsanız, JSON Modu’nu kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="85a8b-143">If you want to statically map the container port to a port on the agent, you need to use JSON Mode.</span></span> <span data-ttu-id="85a8b-144">Bunu yapmak için, geçişi kullanarak Yeni Uygulama Sihirbazı'nı **JSON Modu**’na geçirin.</span><span class="sxs-lookup"><span data-stu-id="85a8b-144">To do so, switch the New Application wizard to **JSON Mode** by using the toggle.</span></span> <span data-ttu-id="85a8b-145">Ardından, uygulama tanımının `portMappings` bölümünün altına aşağıdaki ayarı girin.</span><span class="sxs-lookup"><span data-stu-id="85a8b-145">Then enter the following setting under the `portMappings` section of the application definition.</span></span> <span data-ttu-id="85a8b-146">Bu örnek, kapsayıcının 80 numaralı bağlantı noktasını DC/OS aracının 80 numaralı bağlantı noktasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="85a8b-146">This example binds port 80 of the container to port 80 of the DC/OS agent.</span></span> <span data-ttu-id="85a8b-147">Bu değişikliği yaptıktan sonra bu sihirbazı JSON modundan çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85a8b-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![Yeni Uygulama Kullanıcı Arabirimi--bağlantı noktası 80 örneği](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="85a8b-149">Sistem durumu denetimlerini etkinleştirmek istiyorsanız **Sistem Durumu Denetimleri** sekmesinde bir yol belirleyin.</span><span class="sxs-lookup"><span data-stu-id="85a8b-149">If you want to enable health checks, set a path on the **Health Checks** tab.</span></span>

![Yeni Uygulama UI--durum denetimleri](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="85a8b-151">DC/OS kümesi bir grup özel ve ortak aracıyla dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="85a8b-151">The DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="85a8b-152">Kümenin İnternet’ten uygulamalara erişebilmesi için, uygulamaları ortak aracıya dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="85a8b-152">For the cluster to be able to access applications from the Internet, you need to deploy the applications to a public agent.</span></span> <span data-ttu-id="85a8b-153">Bunu yapmak için, Yeni Uygulama Sihirbazı'nın **İsteğe Bağlı** sekmesini seçin ve **Kabul Edilen Kaynak Rolleri** için **slave_public** girin.</span><span class="sxs-lookup"><span data-stu-id="85a8b-153">To do so, select the **Optional** tab of the New Application wizard and enter **slave_public** for the **Accepted Resource Roles**.</span></span>

<span data-ttu-id="85a8b-154">Ardından **Uygulama Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85a8b-154">Then click **Create Application**.</span></span>

![Yeni Uygulama Kullanıcı Arabirimi--ortak aracı ayarı](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="85a8b-156">Marathon ana sayfasına geri döndüğünüzde, kapsayıcının dağıtımın durumunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85a8b-156">Back on the Marathon main page, you can see the deployment status for the container.</span></span> <span data-ttu-id="85a8b-157">Başlangıçta **Dağıtılıyor** durumu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="85a8b-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="85a8b-158">Dağıtım başarıyla tamamlandıktan sonra durum **Çalışıyor** olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="85a8b-158">After a successful deployment, the status changes to **Running**.</span></span>

![Marathon ana sayfası kullanıcı arabirimi--kapsayıcı dağıtım durumu](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="85a8b-160">DC/OS web kullanıcı arabirimine (http://localhost/) geri döndüğünüzde, bir görevin (örneğimizde, Docker biçimli kapsayıcının) DC/OS kümesinde çalıştığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="85a8b-160">When you switch back to the DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on the DC/OS cluster.</span></span>

![DC/OS web kullanıcı arabirimi--kümede çalışan görev](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="85a8b-162">Görevin üzerinde çalıştığı küme düğümünü görmek için **Düğümler** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85a8b-162">To see the cluster node that the task is running on, click the **Nodes** tab.</span></span>

![DC/OS web kullanıcı arabirimi--görev küme düğümü](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-the-container"></a><span data-ttu-id="85a8b-164">Kapsayıcı ulaşmak</span><span class="sxs-lookup"><span data-stu-id="85a8b-164">Reach the container</span></span>

<span data-ttu-id="85a8b-165">Bu örnekte, uygulamanın bir ortak aracı düğümünde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="85a8b-165">In this example, the application is running on a public agent node.</span></span> <span data-ttu-id="85a8b-166">Küme FQDN'si aracıya göz atarak internet'ten uygulamasına ulaşması: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, burada:</span><span class="sxs-lookup"><span data-stu-id="85a8b-166">You reach the application from the internet by browsing to the agent FQDN of the cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="85a8b-167">**DNSPREFIX** Kümeyi dağıttığınızda sağladığınız DNS önekidir.</span><span class="sxs-lookup"><span data-stu-id="85a8b-167">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>
* <span data-ttu-id="85a8b-168">**REGION** kaynak grubunuzun bulunduğu bölgedir.</span><span class="sxs-lookup"><span data-stu-id="85a8b-168">**REGION** is the region in which your resource group is located.</span></span>

    ![Internet'ten Nginx](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="85a8b-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="85a8b-170">Next steps</span></span>
* [<span data-ttu-id="85a8b-171">DC/OS ve Marathon API’si ile çalışma</span><span class="sxs-lookup"><span data-stu-id="85a8b-171">Work with DC/OS and the Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="85a8b-172">Mesos ile Azure Container Service’e ilişkin ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="85a8b-172">Deep dive on the Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
