---
title: "İzleyici Azure DC/OS kümesi - Datadog | Microsoft Docs"
description: "Azure kapsayıcı hizmeti kümesi Datadog ile izleyin. Kümenize Datadog aracıları dağıtmak için DC/OS web kullanıcı arabirimini kullanın."
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
ms.openlocfilehash: 9dd451f994940d7cc3a59bd7fd08a8f067345e34
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="d3107-105">Azure kapsayıcı hizmeti DC/OS kümesi Datadog ile izleme</span><span class="sxs-lookup"><span data-stu-id="d3107-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="d3107-106">Bu makalede, Azure kapsayıcı hizmeti kümesindeki tüm Aracısı düğümleri biz Datadog aracıları dağıtır.</span><span class="sxs-lookup"><span data-stu-id="d3107-106">In this article we will deploy Datadog agents to all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="d3107-107">Bu yapılandırma için Datadog sahip bir hesap gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3107-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d3107-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d3107-108">Prerequisites</span></span>
<span data-ttu-id="d3107-109">Azure Container Service tarafından yapılandırılmış bir kümeyi [dağıtın](container-service-deployment.md) ve [bağlayın](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d3107-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="d3107-110">[Marathon Kullanıcı Arabirimi](container-service-mesos-marathon-ui.md)’ni keşfedin.</span><span class="sxs-lookup"><span data-stu-id="d3107-110">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="d3107-111">Git [http://datadoghq.com](http://datadoghq.com) bir Datadog hesabı ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="d3107-111">Go to [http://datadoghq.com](http://datadoghq.com) to set up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="d3107-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="d3107-112">Datadog</span></span>
<span data-ttu-id="d3107-113">Datadog, Azure kapsayıcı hizmeti kümesi kapsayıcılara gelen izleme verilerini toplayan izleme bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="d3107-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="d3107-114">Datadog Docker tümleştirmesi, kapsayıcılara belirli ölçümleri görebileceğiniz bir Pano vardır.</span><span class="sxs-lookup"><span data-stu-id="d3107-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="d3107-115">Kapsayıcılardan toplanan ölçümleri CPU, bellek, ağ ve g/ç tarafından düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="d3107-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="d3107-116">Datadog ölçümleri kapsayıcıları ve görüntüleri halinde ayırır.</span><span class="sxs-lookup"><span data-stu-id="d3107-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="d3107-117">Kullanıcı arabirimini nasıl için CPU kullanımını göründüğünü örneği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d3107-117">An example of what the UI looks like for CPU usage is below.</span></span>

![Datadog kullanıcı Arabirimi](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="d3107-119">Marathon ile Datadog dağıtımını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d3107-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="d3107-120">Bu adımları yapılandırmak ve Marathon kümenizle Datadog uygulamaları dağıtmak nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3107-120">These steps will show you how to configure and deploy Datadog applications to your cluster with Marathon.</span></span> 

<span data-ttu-id="d3107-121">DC/OS kullanıcı Arabirimi aracılığıyla erişim [http://localhost:80 /](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="d3107-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="d3107-122">DC/OS kullanıcı Arabiriminde "sol alta olan Universe" kez gidin ve "Datadog" için arama yapın ve "Yükle" yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d3107-122">Once in the DC/OS UI navigate to the "Universe" which is on the bottom left and then search for "Datadog" and click "Install."</span></span>

![Datadog paket DC/OS Universe içinde](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="d3107-124">Şimdi yapılandırmasını tamamlamak için bir Datadog hesap veya ücretsiz bir deneme hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3107-124">Now to complete the configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="d3107-125">Sol Datadog Web sitesi görünüm için oturum açtınız ve tümleştirmeler gidin sonra sonra -> [API'leri](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="d3107-125">Once you're logged in to the Datadog website look to the left and go to Integrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Datadog API anahtarı](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="d3107-127">Sonraki DC/OS Universe içinde Datadog yapılandırma içine API anahtarınızı girin.</span><span class="sxs-lookup"><span data-stu-id="d3107-127">Next enter your API key into the Datadog configuration within the DC/OS Universe.</span></span> 

![DC/OS Universe Datadog yapılandırma](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="d3107-129">Yukarıdaki yapılandırmada örnekleri 10000000 için ayarlanmış olan bunu yeni bir düğüm kümeye Datadog otomatik olarak bu düğüme bir aracı dağıtacağınız eklendiği zaman.</span><span class="sxs-lookup"><span data-stu-id="d3107-129">In the above configuration instances are set to 10000000 so whenever a new node is added to the cluster Datadog will automatically deploy an agent to that node.</span></span> <span data-ttu-id="d3107-130">Bu geçici bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="d3107-130">This is an interim solution.</span></span> <span data-ttu-id="d3107-131">Tekrar Datadog Web sitesine gidin ve bulmak paketini yükledikten sonra "[panolar](https://app.datadoghq.com/dash/list)."</span><span class="sxs-lookup"><span data-stu-id="d3107-131">Once you've installed the package you should navigate back to the Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="d3107-132">Buradan, özel ve tümleştirme panolar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d3107-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="d3107-133">[Docker Pano](https://app.datadoghq.com/screen/integration/docker) kümenizi izleme için gereksinim duyduğunuz tüm kapsayıcı ölçümleri sahip olur.</span><span class="sxs-lookup"><span data-stu-id="d3107-133">The [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all the container metrics you need for monitoring your cluster.</span></span> 

