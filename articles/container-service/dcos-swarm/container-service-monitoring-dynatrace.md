---
title: "aaaMonitor Azure DC/OS kümesi - Dynatrace | Microsoft Docs"
description: "Azure kapsayıcı hizmeti DC/OS kümesi Dynatrace ile izleyin. Merhaba Dynatrace OneAgent hello DC/OS panosunu kullanarak dağıtın."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="791f2-105">Azure kapsayıcı hizmeti DC/OS kümesi Dynatrace SaaS/yönetilen'ile izleme</span><span class="sxs-lookup"><span data-stu-id="791f2-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="791f2-106">Bu makalede, nasıl gösteriyoruz toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor tüm hello Azure kapsayıcı hizmeti kümenizdeki düğümlerin Aracısı.</span><span class="sxs-lookup"><span data-stu-id="791f2-106">In this article, we show you how toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor all hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="791f2-107">Bu yapılandırma için bir hesap ile Dynatrace SaaS/yönetilen gerekir.</span><span class="sxs-lookup"><span data-stu-id="791f2-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="791f2-108">Dynatrace SaaS/yönetilen</span><span class="sxs-lookup"><span data-stu-id="791f2-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="791f2-109">Dynatrace bir bulut yerel izleme için yüksek oranda dinamik kapsayıcı ve küme ortamları çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="791f2-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="791f2-110">Bu sayede toobetter en iyi duruma getirme kapsayıcı dağıtımlarını ve bellek ayırma gerçek zamanlı kullanım verilerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="791f2-110">It allows you toobetter optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="791f2-111">Otomatik olarak uygulama ve altyapı sorunları otomatik taban çizgisi oluşturma, sorunu bağıntı ve temel nedenin algılama sağlayarak yerini tam olarak belirtmekte yeteneğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="791f2-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="791f2-112">Merhaba aşağıdaki gösterir hello Dynatrace UI şekil:</span><span class="sxs-lookup"><span data-stu-id="791f2-112">hello following figure shows hello Dynatrace UI:</span></span>

![Dynatrace kullanıcı Arabirimi](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="791f2-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="791f2-114">Prerequisites</span></span> 
<span data-ttu-id="791f2-115">[Dağıtma](container-service-deployment.md) ve [bağlanmak](./../container-service-connect.md) tooa küme Azure kapsayıcı hizmeti tarafından yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="791f2-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) tooa cluster configured by Azure Container Service.</span></span> <span data-ttu-id="791f2-116">Merhaba keşfedin [Marathon kullanıcı Arabirimi](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="791f2-116">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="791f2-117">Çok Git[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset Dynatrace SaaS hesabı.</span><span class="sxs-lookup"><span data-stu-id="791f2-117">Go too[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="791f2-118">Marathon ile Dynatrace dağıtımını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="791f2-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="791f2-119">Bu adımlar şunları nasıl yapacağınızı tooconfigure ve Dynatrace uygulamaları tooyour küme Marathon ile dağıtın.</span><span class="sxs-lookup"><span data-stu-id="791f2-119">These steps show you how tooconfigure and deploy Dynatrace applications tooyour cluster with Marathon.</span></span>

1. <span data-ttu-id="791f2-120">DC/OS kullanıcı Arabirimi aracılığıyla erişim [http://localhost:80 /](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="791f2-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="791f2-121">Bir kez hello DC/OS kullanıcı Arabirimi, toohello gidin **Universe** sekmesinde arayın ve sonra **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="791f2-121">Once in hello DC/OS UI, navigate toohello **Universe** tab and then search for **Dynatrace**.</span></span>

    ![DC/OS Universe Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="791f2-123">toocomplete hello yapılandırması, bir Dynatrace SaaS hesap veya ücretsiz bir deneme hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="791f2-123">toocomplete hello configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="791f2-124">Merhaba Dynatrace panoya oturum sonra seçeneğini **dağıtmak Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="791f2-124">Once you log into hello Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![PaaS tümleştirme Dynatrace ayarlama](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="791f2-126">Merhaba sayfasında seçin **PaaS tümleştirmesini ayarlama**.</span><span class="sxs-lookup"><span data-stu-id="791f2-126">On hello page, select **Set up PaaS integration**.</span></span> 

    ![Dynatrace API belirteci](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="791f2-128">Merhaba Dynatrace OneAgent yapılandırma hello DC/OS Universe içinde içine API belirtecinizi girin.</span><span class="sxs-lookup"><span data-stu-id="791f2-128">Enter your API token into hello Dynatrace OneAgent configuration within hello DC/OS Universe.</span></span> 

    ![Merhaba DC/OS Universe Dynatrace OneAgent yapılandırma](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="791f2-130">Merhaba örnekleri kümesi toohello numarası toorun düşündüğünüz düğümlerinin.</span><span class="sxs-lookup"><span data-stu-id="791f2-130">Set hello instances toohello number of nodes you intend toorun.</span></span> <span data-ttu-id="791f2-131">Bu sayıyı gerçekte ulaşılana kadar daha yüksek bir sayı çalışır, ancak DC/OS ayarı toofind yeni örnekleri denemeye devam edilecek.</span><span class="sxs-lookup"><span data-stu-id="791f2-131">Setting a higher number also works, but DC/OS will keep trying toofind new instances until that number is actually reached.</span></span> <span data-ttu-id="791f2-132">Tercih ederseniz, bu tooa değer 1000000 gibi de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="791f2-132">If you prefer, you can also set this tooa value like 1000000.</span></span> <span data-ttu-id="791f2-133">Bu durumda, yeni bir düğüm toohello küme eklendiğinde Dynatrace otomatik olarak bir aracı toothat yeni düğümü, DC/OS sürekli toodeploy başka örnekler çalışıyor hello fiyatla dağıtır.</span><span class="sxs-lookup"><span data-stu-id="791f2-133">In this case, whenever a new node is added toohello cluster, Dynatrace automatically deploys an agent toothat new node, at hello price of DC/OS constantly trying toodeploy further instances.</span></span>

    ![Merhaba DC/OS Universe-örnekleri Dynatrace yapılandırma](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="791f2-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="791f2-135">Next steps</span></span>

<span data-ttu-id="791f2-136">Merhaba paketini yükledikten sonra geri toohello Dynatrace Pano gidin.</span><span class="sxs-lookup"><span data-stu-id="791f2-136">Once you've installed hello package, navigate back toohello Dynatrace dashboard.</span></span> <span data-ttu-id="791f2-137">Küme içinde Merhaba kapsayıcılara için hello farklı kullanım ölçümleri gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="791f2-137">You can explore hello different usage metrics for hello containers within your cluster.</span></span> 
