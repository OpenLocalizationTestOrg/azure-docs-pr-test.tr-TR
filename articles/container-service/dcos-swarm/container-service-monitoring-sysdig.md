---
title: "aaaMonitor bir Azure kapsayıcı hizmeti kümesi ile Sysdig | Microsoft Docs"
description: "Sysdig ile bir Azure Container Service kümesini izleyin."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="76bfc-104">Sysdig ile bir Azure Container Service kümesini izleme</span><span class="sxs-lookup"><span data-stu-id="76bfc-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="76bfc-105">Bu makalede, sizi Azure kapsayıcı hizmeti kümenizdeki Sysdig aracıları tooall hello Aracısı düğümlerin dağıtır.</span><span class="sxs-lookup"><span data-stu-id="76bfc-105">In this article, we will deploy Sysdig agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="76bfc-106">Bu yapılandırma için bir Sysdig hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="76bfc-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="76bfc-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="76bfc-107">Prerequisites</span></span>
<span data-ttu-id="76bfc-108">Azure Container Service tarafından yapılandırılmış bir kümeyi [dağıtın](container-service-deployment.md) ve [bağlayın](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="76bfc-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="76bfc-109">Merhaba keşfedin [Marathon kullanıcı Arabirimi](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="76bfc-109">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="76bfc-110">Çok Git[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset Sysdig bulut hesabı.</span><span class="sxs-lookup"><span data-stu-id="76bfc-110">Go too[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="76bfc-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="76bfc-111">Sysdig</span></span>
<span data-ttu-id="76bfc-112">Sysdig olan toomonitor sağlayan bir izleme hizmeti, kümenizi kapsayıcılara.</span><span class="sxs-lookup"><span data-stu-id="76bfc-112">Sysdig is a monitoring service that allows you toomonitor your containers within your cluster.</span></span> <span data-ttu-id="76bfc-113">Sorun giderme toohelp Sysdig bilinir ancak aynı zamanda temel izleme ölçümlerinizi CPU, ağ, bellek ve g/ç için bulunur.</span><span class="sxs-lookup"><span data-stu-id="76bfc-113">Sysdig is known toohelp with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="76bfc-114">Sysdig kapsayıcıları çalıştığınız kolay toosee kılar hardest veya temelde kullanarak hello hello çoğu bellek ve CPU.</span><span class="sxs-lookup"><span data-stu-id="76bfc-114">Sysdig makes it easy toosee which containers are working hello hardest or essentially using hello most memory and CPU.</span></span> <span data-ttu-id="76bfc-115">Merhaba, "şu an beta genel bakış" bölümünde, bu görünüm kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="76bfc-115">This view is in hello “Overview” section, which is currently in beta.</span></span> 

![Sysdig Kullanıcı Arabirimi](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="76bfc-117">Marathon ile bir Sysdig dağıtımı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="76bfc-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="76bfc-118">Bu adımlar şunları nasıl yapacağınızı gösterilecek tooconfigure ve Sysdig uygulamaları tooyour küme Marathon ile dağıtın.</span><span class="sxs-lookup"><span data-stu-id="76bfc-118">These steps will show you how tooconfigure and deploy Sysdig applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="76bfc-119">DC/OS kullanıcı Arabirimi aracılığıyla erişim [http://localhost:80 /](http://localhost:80/) kez hello DC/OS kullanıcı Arabirimi hello üzerinde olan "Universe" sol alt ve "Sysdig" için arama toohello gidin</span><span class="sxs-lookup"><span data-stu-id="76bfc-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate toohello "Universe", which is on hello bottom left and then search for "Sysdig."</span></span>

![DC/OS Evreninde Sysdig](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="76bfc-121">Şimdi, bir Sysdig gerek toocomplete hello yapılandırma hesap veya ücretsiz bir deneme hesabı bulut.</span><span class="sxs-lookup"><span data-stu-id="76bfc-121">Now toocomplete hello configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="76bfc-122">Toohello Sysdig bulut Web sitesinde oturum açtınız sonra kullanıcı adına tıklayın ve hello sayfasında "Erişim anahtarınızı." görmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="76bfc-122">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Sysdig API anahtarı](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="76bfc-124">Sonraki hello Sysdig yapılandırma hello DC/OS Universe içinde uygulamasına erişim anahtarınızı girin.</span><span class="sxs-lookup"><span data-stu-id="76bfc-124">Next enter your Access Key into hello Sysdig configuration within hello DC/OS Universe.</span></span> 

![Merhaba DC/OS Universe Sysdig yapılandırma](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="76bfc-126">Şimdi yeni bir düğüm eklendiğinde toohello küme Sysdig otomatik olarak bir aracı dağıtmak için hello örnekleri too10000000 toothat yeni düğüm kümesi.</span><span class="sxs-lookup"><span data-stu-id="76bfc-126">Now set hello instances too10000000 so whenever a new node is added toohello cluster Sysdig will automatically deploy an agent toothat new node.</span></span> <span data-ttu-id="76bfc-127">Bu, bir geçici çözüm toomake Sysdig tooall yeni hello küme aracılarına dağıtacağınız emin olur.</span><span class="sxs-lookup"><span data-stu-id="76bfc-127">This is an interim solution toomake sure Sysdig will deploy tooall new agents within hello cluster.</span></span> 

![Merhaba DC/OS Universe-örnekleri Sysdig yapılandırma](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="76bfc-129">Merhaba paketini yükledikten sonra geri toohello Sysdig UI gidin ve küme içinde Merhaba kapsayıcılara için mümkün tooexplore hello farklı kullanım ölçümleri olması.</span><span class="sxs-lookup"><span data-stu-id="76bfc-129">Once you've installed hello package navigate back toohello Sysdig UI and you'll be able tooexplore hello different usage metrics for hello containers within your cluster.</span></span> 

<span data-ttu-id="76bfc-130">Ayrıca [yeni pano sihirbazıyla](https://app.sysdigcloud.com/#/dashboards/new) Mesos ve Marathon'a özel panoları da yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76bfc-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
