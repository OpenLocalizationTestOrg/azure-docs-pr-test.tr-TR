---
title: "aaaMonitor Azure DC/OS kümesi - Datadog | Microsoft Docs"
description: "Azure kapsayıcı hizmeti kümesi Datadog ile izleyin. Merhaba DC/OS web kullanıcı Arabirimi toodeploy hello Datadog aracıları tooyour kümesi kullanın."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, DC/OS, Docker Swarm, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="2d8a7-105">Azure kapsayıcı hizmeti DC/OS kümesi Datadog ile izleme</span><span class="sxs-lookup"><span data-stu-id="2d8a7-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="2d8a7-106">Bu makalede biz Datadog aracıları tooall hello Aracısı düğümleri, Azure kapsayıcı hizmeti kümesi dağıtır.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-106">In this article we will deploy Datadog agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="2d8a7-107">Bu yapılandırma için Datadog sahip bir hesap gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2d8a7-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2d8a7-108">Prerequisites</span></span>
<span data-ttu-id="2d8a7-109">Azure Container Service tarafından yapılandırılmış bir kümeyi [dağıtın](container-service-deployment.md) ve [bağlayın](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="2d8a7-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="2d8a7-110">Merhaba keşfedin [Marathon kullanıcı Arabirimi](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="2d8a7-110">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="2d8a7-111">Çok Git[http://datadoghq.com](http://datadoghq.com) tooset Datadog hesabı.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-111">Go too[http://datadoghq.com](http://datadoghq.com) tooset up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="2d8a7-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="2d8a7-112">Datadog</span></span>
<span data-ttu-id="2d8a7-113">Datadog, Azure kapsayıcı hizmeti kümesi kapsayıcılara gelen izleme verilerini toplayan izleme bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="2d8a7-114">Datadog Docker tümleştirmesi, kapsayıcılara belirli ölçümleri görebileceğiniz bir Pano vardır.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="2d8a7-115">Kapsayıcılardan toplanan ölçümleri CPU, bellek, ağ ve g/ç tarafından düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="2d8a7-116">Datadog ölçümleri kapsayıcıları ve görüntüleri halinde ayırır.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="2d8a7-117">Hangi hello örneği için CPU kullanımı aşağıdadır UI görülüyor.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-117">An example of what hello UI looks like for CPU usage is below.</span></span>

![Datadog kullanıcı Arabirimi](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="2d8a7-119">Marathon ile Datadog dağıtımını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2d8a7-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="2d8a7-120">Bu adımlar şunları nasıl yapacağınızı gösterilecek tooconfigure ve Datadog uygulamaları tooyour küme Marathon ile dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-120">These steps will show you how tooconfigure and deploy Datadog applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="2d8a7-121">DC/OS kullanıcı Arabirimi aracılığıyla erişim [http://localhost:80 /](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="2d8a7-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="2d8a7-122">Bir kez DC/OS kullanıcı Arabirimi gidin hello toohello "Merhaba üzerinde olan Universe" sol alt ve "Datadog" için arama yapın ve "Yükle" yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-122">Once in hello DC/OS UI navigate toohello "Universe" which is on hello bottom left and then search for "Datadog" and click "Install."</span></span>

![Datadog paket hello DC/OS Universe içinde](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="2d8a7-124">Toocomplete hello artık yapılandırma Datadog hesap veya ücretsiz bir deneme hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-124">Now toocomplete hello configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="2d8a7-125">Oturum açtınız sonra toohello sol toohello Datadog Web sitesine bakın ve Git tooIntegrations -> sonra [API'leri](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="2d8a7-125">Once you're logged in toohello Datadog website look toohello left and go tooIntegrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Datadog API anahtarı](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="2d8a7-127">Sonraki hello Datadog yapılandırma hello DC/OS Universe içinde içine API anahtarınızı girin.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-127">Next enter your API key into hello Datadog configuration within hello DC/OS Universe.</span></span> 

![Merhaba DC/OS Universe Datadog yapılandırma](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="2d8a7-129">Yeni bir düğüm eklendiğinde toohello küme Datadog otomatik olarak bir aracı toothat düğümüne dağıtacak şekilde hello yapılandırma yukarıda örnekleri too10000000 ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-129">In hello above configuration instances are set too10000000 so whenever a new node is added toohello cluster Datadog will automatically deploy an agent toothat node.</span></span> <span data-ttu-id="2d8a7-130">Bu geçici bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-130">This is an interim solution.</span></span> <span data-ttu-id="2d8a7-131">Merhaba paketini yükledikten sonra geri toohello Datadog Web sitesine gidin ve bulmak gerekir "[panolar](https://app.datadoghq.com/dash/list)."</span><span class="sxs-lookup"><span data-stu-id="2d8a7-131">Once you've installed hello package you should navigate back toohello Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="2d8a7-132">Buradan, özel ve tümleştirme panolar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="2d8a7-133">Merhaba [Docker Pano](https://app.datadoghq.com/screen/integration/docker) kümenizi izleme için gereksinim duyduğunuz tüm hello kapsayıcı ölçümleri sahip olur.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-133">hello [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all hello container metrics you need for monitoring your cluster.</span></span> 

