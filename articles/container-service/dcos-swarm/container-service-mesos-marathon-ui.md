---
title: "aaaManage Azure DC/OS kümesi Marathon kullanıcı Arabirimi ile | Microsoft Docs"
description: "Kapsayıcıları tooan Azure kapsayıcı hizmeti Küme hizmetine hello Marathon web kullanıcı arabirimini kullanarak dağıtın."
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
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a><span data-ttu-id="9fd01-104">Azure kapsayıcı hizmeti DC/OS kümesi hello Marathon web kullanıcı Arabirimi üzerinden yönetmek</span><span class="sxs-lookup"><span data-stu-id="9fd01-104">Manage an Azure Container Service DC/OS cluster through hello Marathon web UI</span></span>
<span data-ttu-id="9fd01-105">DC/OS dağıtma ve hello temel donanımı özetlerken, kümelenmiş iş yükleri ölçekleme için bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="9fd01-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="9fd01-106">DC/OS’nin en üstünde, hesaplama iş yüklerini zamanlamayı ve yürütmeyi yöneten bir çerçeve vardır.</span><span class="sxs-lookup"><span data-stu-id="9fd01-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="9fd01-107">Çerçeveler çok sayıda yaygın iş yükü için kullanılabilir, ancak bu belgede Marathon ile kapsayıcı dağıtma tooget nasıl başlatılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="9fd01-107">While frameworks are available for many popular workloads, this document describes how tooget started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="9fd01-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9fd01-108">Prerequisites</span></span>
<span data-ttu-id="9fd01-109">Bu örneklerin üzerinden geçmeden önce, Azure Kapsayıcı Hizmeti’nde yapılandırılan bir DC/OS kümeniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fd01-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="9fd01-110">Ayrıca toohave uzak bağlantı toothis küme gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fd01-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="9fd01-111">Bu öğeler hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="9fd01-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="9fd01-112">Azure Container Service kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="9fd01-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="9fd01-113">Tooan Azure kapsayıcı hizmeti kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="9fd01-113">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="9fd01-114">Bu makalede, yerel bağlantı noktası 80 üzerinden toohello DC/OS kümesine tünel varsayar.</span><span class="sxs-lookup"><span data-stu-id="9fd01-114">This article assumes you are tunneling toohello DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-hello-dcos-ui"></a><span data-ttu-id="9fd01-115">Merhaba DC/OS kullanıcı arabirimini keşfetme</span><span class="sxs-lookup"><span data-stu-id="9fd01-115">Explore hello DC/OS UI</span></span>
<span data-ttu-id="9fd01-116">Secure Shell (SSH) tüneli ile [kurulan](../container-service-connect.md), toohttp://localhost/ göz atın.</span><span class="sxs-lookup"><span data-stu-id="9fd01-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse toohttp://localhost/.</span></span> <span data-ttu-id="9fd01-117">Bu hello DC/OS web kullanıcı arabirimini yükler ve kullanılan kaynaklar, etkin aracılar ve çalışan hizmetler gibi hello küme hakkında bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="9fd01-117">This loads hello DC/OS web UI and shows information about hello cluster, such as used resources, active agents, and running services.</span></span>

![DC/OS Kullanıcı Arabirimi](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a><span data-ttu-id="9fd01-119">Merhaba Marathon kullanıcı arabirimini keşfetme</span><span class="sxs-lookup"><span data-stu-id="9fd01-119">Explore hello Marathon UI</span></span>
<span data-ttu-id="9fd01-120">toosee hello Marathon kullanıcı Arabirimi, toohttp://localhost/marathon göz atın.</span><span class="sxs-lookup"><span data-stu-id="9fd01-120">toosee hello Marathon UI, browse toohttp://localhost/marathon.</span></span> <span data-ttu-id="9fd01-121">Bu ekranda hello Azure kapsayıcı hizmeti DC/OS kümesinde yeni bir kapsayıcı veya başka bir uygulama başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fd01-121">From this screen, you can start a new container or another application on hello Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="9fd01-122">Kapsayıcıları ve uygulamaları çalıştırma hakkında bilgileri de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fd01-122">You can also see information about running containers and applications.</span></span>  

![Marathon kullanıcı arabirimi](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="9fd01-124">Docker biçimli kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="9fd01-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="9fd01-125">toodeploy Marathon, kullanarak yeni bir kapsayıcı tıklatın **uygulama oluştur**ve hello form sekmelere bilgisinden hello girin:</span><span class="sxs-lookup"><span data-stu-id="9fd01-125">toodeploy a new container by using Marathon, click **Create Application**, and enter hello following information into hello form tabs:</span></span>

| <span data-ttu-id="9fd01-126">Alan</span><span class="sxs-lookup"><span data-stu-id="9fd01-126">Field</span></span> | <span data-ttu-id="9fd01-127">Değer</span><span class="sxs-lookup"><span data-stu-id="9fd01-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9fd01-128">Kimlik</span><span class="sxs-lookup"><span data-stu-id="9fd01-128">ID</span></span> |<span data-ttu-id="9fd01-129">nginx</span><span class="sxs-lookup"><span data-stu-id="9fd01-129">nginx</span></span> |
| <span data-ttu-id="9fd01-130">Bellek</span><span class="sxs-lookup"><span data-stu-id="9fd01-130">Memory</span></span> | <span data-ttu-id="9fd01-131">32</span><span class="sxs-lookup"><span data-stu-id="9fd01-131">32</span></span> |
| <span data-ttu-id="9fd01-132">Görüntü</span><span class="sxs-lookup"><span data-stu-id="9fd01-132">Image</span></span> |<span data-ttu-id="9fd01-133">nginx</span><span class="sxs-lookup"><span data-stu-id="9fd01-133">nginx</span></span> |
| <span data-ttu-id="9fd01-134">Ağ</span><span class="sxs-lookup"><span data-stu-id="9fd01-134">Network</span></span> |<span data-ttu-id="9fd01-135">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="9fd01-135">Bridged</span></span> |
| <span data-ttu-id="9fd01-136">Ana Bilgisayar Bağlantı Noktası</span><span class="sxs-lookup"><span data-stu-id="9fd01-136">Host Port</span></span> |<span data-ttu-id="9fd01-137">80</span><span class="sxs-lookup"><span data-stu-id="9fd01-137">80</span></span> |
| <span data-ttu-id="9fd01-138">Protokol</span><span class="sxs-lookup"><span data-stu-id="9fd01-138">Protocol</span></span> |<span data-ttu-id="9fd01-139">TCP</span><span class="sxs-lookup"><span data-stu-id="9fd01-139">TCP</span></span> |

![Yeni Uygulama Kullanıcı Arabirimi --Genel](./media/container-service-mesos-marathon-ui/dcos4.png)

![Yeni Uygulama Kullanıcı Arabirimi--Docker Kapsayıcısı](./media/container-service-mesos-marathon-ui/dcos5.png)

![Yeni Uygulama Kullanıcı Arabirimi--Bağlantı Noktaları ve Hizmet Bulma](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="9fd01-143">Toostatically harita hello kapsayıcı bağlantı noktası tooa bağlantı noktası üzerinde hello Aracısı istiyorsanız toouse JSON modu gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fd01-143">If you want toostatically map hello container port tooa port on hello agent, you need toouse JSON Mode.</span></span> <span data-ttu-id="9fd01-144">toodo bu nedenle, geçiş hello yeni uygulama Sihirbazı'nı çok**JSON modu** hello geçiş kullanarak.</span><span class="sxs-lookup"><span data-stu-id="9fd01-144">toodo so, switch hello New Application wizard too**JSON Mode** by using hello toggle.</span></span> <span data-ttu-id="9fd01-145">Ayarı hello altında aşağıdaki hello enter `portMappings` hello uygulama tanımının bölümü.</span><span class="sxs-lookup"><span data-stu-id="9fd01-145">Then enter hello following setting under hello `portMappings` section of hello application definition.</span></span> <span data-ttu-id="9fd01-146">Bu örnek hello DC/OS aracının 80 hello kapsayıcı tooport bağlantı noktası 80 bağlar.</span><span class="sxs-lookup"><span data-stu-id="9fd01-146">This example binds port 80 of hello container tooport 80 of hello DC/OS agent.</span></span> <span data-ttu-id="9fd01-147">Bu değişikliği yaptıktan sonra bu sihirbazı JSON modundan çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fd01-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![Yeni Uygulama Kullanıcı Arabirimi--bağlantı noktası 80 örneği](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="9fd01-149">Tooenable durumu denetimleri istiyorsanız, bir yol hello ayarlayın **sistem durumu denetler** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9fd01-149">If you want tooenable health checks, set a path on hello **Health Checks** tab.</span></span>

![Yeni Uygulama UI--durum denetimleri](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="9fd01-151">Merhaba DC/OS kümesi özel ve ortak aracıyla kümesiyle dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="9fd01-151">hello DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="9fd01-152">Merhaba küme toobe mümkün tooaccess uygulamalardan için hello Internet toodeploy hello uygulamaları tooa ortak Aracı gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fd01-152">For hello cluster toobe able tooaccess applications from hello Internet, you need toodeploy hello applications tooa public agent.</span></span> <span data-ttu-id="9fd01-153">toodo, bu nedenle, hello seçin **isteğe bağlı** sekmesini hello yeni uygulama Sihirbazı'nın ve girin **slave_public** hello için **kabul edilen kaynak rolleri**.</span><span class="sxs-lookup"><span data-stu-id="9fd01-153">toodo so, select hello **Optional** tab of hello New Application wizard and enter **slave_public** for hello **Accepted Resource Roles**.</span></span>

<span data-ttu-id="9fd01-154">Ardından **Uygulama Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9fd01-154">Then click **Create Application**.</span></span>

![Yeni Uygulama Kullanıcı Arabirimi--ortak aracı ayarı](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="9fd01-156">Geri hello Marathon ana sayfasına hello kapsayıcı hello dağıtım durumunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fd01-156">Back on hello Marathon main page, you can see hello deployment status for hello container.</span></span> <span data-ttu-id="9fd01-157">Başlangıçta **Dağıtılıyor** durumu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9fd01-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="9fd01-158">Başarılı dağıtım sonrasında, durum değişikliklerini çok hello**çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="9fd01-158">After a successful deployment, hello status changes too**Running**.</span></span>

![Marathon ana sayfası kullanıcı arabirimi--kapsayıcı dağıtım durumu](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="9fd01-160">Geri toohello DC/OS web kullanıcı Arabirimine (http://localhost/) geçiş yaptığınızda, bir görevin (örneğimizde, Docker biçimli kapsayıcının) hello DC/OS kümesinde çalıştığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9fd01-160">When you switch back toohello DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on hello DC/OS cluster.</span></span>

![DC/OS web kullanıcı Arabirimi--hello kümede çalışan görev](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="9fd01-162">Görev hello toosee hello küme düğümü üzerinde çalıştığından, hello tıklatın **düğümleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9fd01-162">toosee hello cluster node that hello task is running on, click hello **Nodes** tab.</span></span>

![DC/OS web kullanıcı arabirimi--görev küme düğümü](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a><span data-ttu-id="9fd01-164">Merhaba kapsayıcı ulaşmak</span><span class="sxs-lookup"><span data-stu-id="9fd01-164">Reach hello container</span></span>

<span data-ttu-id="9fd01-165">Bu örnekte, bir ortak aracı düğümünde Merhaba uygulaması çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="9fd01-165">In this example, hello application is running on a public agent node.</span></span> <span data-ttu-id="9fd01-166">Merhaba hello uygulamadan ulaşmak toohello Aracısı hello küme FQDN'si giderek Internet: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, burada:</span><span class="sxs-lookup"><span data-stu-id="9fd01-166">You reach hello application from hello internet by browsing toohello agent FQDN of hello cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="9fd01-167">**DNSPREFIX** hello kümeyi dağıttığınızda sağladığınız hello DNS önekidir.</span><span class="sxs-lookup"><span data-stu-id="9fd01-167">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>
* <span data-ttu-id="9fd01-168">**Bölge** kaynak grubunuzun bulunduğu hello bölgedir.</span><span class="sxs-lookup"><span data-stu-id="9fd01-168">**REGION** is hello region in which your resource group is located.</span></span>

    ![Internet'ten Nginx](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="9fd01-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9fd01-170">Next steps</span></span>
* [<span data-ttu-id="9fd01-171">Marathon API'si hello ve DC/OS ile çalışma</span><span class="sxs-lookup"><span data-stu-id="9fd01-171">Work with DC/OS and hello Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="9fd01-172">Azure kapsayıcı hizmeti Mesos ile Merhaba üzerinde derin Dalış</span><span class="sxs-lookup"><span data-stu-id="9fd01-172">Deep dive on hello Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
