---
title: "aaaMonitor Azure DC/OS kümesi - Operations Management | Microsoft Docs"
description: "Microsoft Operations Management Suite ile Azure kapsayıcı hizmeti DC/OS kümesi izleyin."
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="6e5f1-103">Operations Management Suite ile Azure kapsayıcı hizmeti DC/OS kümesi izleme</span><span class="sxs-lookup"><span data-stu-id="6e5f1-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="6e5f1-104">Microsoft Operations Management Suite (OMS), şirket içi ve bulut altyapınızı yönetmenize ve korumanıza yardımcı olan, Microsoft'un bulut tabanlı BT yönetim çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="6e5f1-105">Kapsayıcı, bir çözümde hello kapsayıcı envanterini görüntüleme, performans ve günlükleri tek bir konumda yardımcı olan OMS günlük analizi çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-105">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="6e5f1-106">Denetim, merkezi konumda hello günlükleri görüntüleyerek kapsayıcıları sorun giderme ve bir ana bilgisayar üzerindeki fazladan kapsayıcı tüketen gürültülü bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-106">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="6e5f1-107">Kapsayıcı çözüm hakkında daha fazla bilgi için lütfen toothe bakın [kapsayıcı çözüm günlük analizi](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="6e5f1-107">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-hello-dcos-universe"></a><span data-ttu-id="6e5f1-108">OMS hello DC/OS universe'ten ayarlama</span><span class="sxs-lookup"><span data-stu-id="6e5f1-108">Setting up OMS from hello DC/OS universe</span></span>


<span data-ttu-id="6e5f1-109">Bu makalede bir DC/OS ayarladıktan ve basit bir web kapsayıcı uygulamaları hello kümede dağıtmış olan varsayar.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on hello cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="6e5f1-110">Önkoşul</span><span class="sxs-lookup"><span data-stu-id="6e5f1-110">Pre-requisite</span></span>
- <span data-ttu-id="6e5f1-111">[Microsoft Azure aboneliği](https://azure.microsoft.com/free/) -bu ücretsiz alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="6e5f1-112">Microsoft OMS çalışma Kurulumu - bkz aşağıda "Adım 3"</span><span class="sxs-lookup"><span data-stu-id="6e5f1-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="6e5f1-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) yüklü.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="6e5f1-114">Merhaba DC/OS panosunda Universe ve 'aşağıda gösterildiği gibi OMS' araması tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-114">In hello DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="6e5f1-115">**Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-115">Click **Install**.</span></span> <span data-ttu-id="6e5f1-116">Merhaba OMS sürüm bilgilerle yukarı pop görürsünüz ve bir **paket yükleme** veya **gelişmiş yükleme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-116">You will see a pop up with hello OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="6e5f1-117">Tıkladığınızda **gelişmiş yükleme**, hangi müşteri adayları, toohello **OMS belirli yapılandırma özellikleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-117">When you click **Advanced Installation**, which leads you toohello **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="6e5f1-118">Burada, tooenter hello sizden istenir `wsid` (OMS çalışma alanı kimliği hello) ve `wskey` (Merhaba OMS birincil anahtar hello çalışma alanı kimliği için).</span><span class="sxs-lookup"><span data-stu-id="6e5f1-118">Here, you will be asked tooenter hello `wsid` (hello OMS workspace ID) and `wskey` (hello OMS primary key for hello workspace id).</span></span> <span data-ttu-id="6e5f1-119">Her iki tooget `wsid` ve `wskey` OMS hesabı toocreate gerek <https://mms.microsoft.com>. Lütfen başlangıç adımları toocreate bir hesap izleyin.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-119">tooget both `wsid` and `wskey` you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="6e5f1-120">Merhaba hesabı oluşturulurken tamamladıktan sonra tooobtain gerekir, `wsid` ve `wskey` tıklayarak **ayarları**, ardından **bağlı kaynakları**ve ardından **Linux sunucuları** , aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-120">Once you are done creating hello account, you need tooobtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="6e5f1-121">İstediğiniz ve hello 'Gözden geçirin ve yükleyin' düğmesini tıklatın hello numara, OMS örneği seçin.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-121">Select hello number you OMS instances that you want and click hello ‘Review and Install’ button.</span></span> <span data-ttu-id="6e5f1-122">Genellikle, toohave hello sayısının OMS örnekleri eşit toohello Aracısı kümenizdeki sahip VM'in isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-122">Typically, you will want toohave hello number of OMS instances equal toohello number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="6e5f1-123">Linux için OMS aracısının toocollect bilgilerini izleme ve günlük bilgilerini istiyorsa, her bir VM üzerinde tek tek kapsayıcıları yükler gibidir.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-123">OMS Agent for Linux is installs as individual containers on each VM that it wants toocollect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="6e5f1-124">Basit bir OMS Pano ayarlama</span><span class="sxs-lookup"><span data-stu-id="6e5f1-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="6e5f1-125">Linux hello VM'ler için hello OMS Aracısı yüklendiğinde sonraki hello OMS Pano yukarı tooset adımdır.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-125">Once you have installed hello OMS Agent for Linux on hello VMs, next step is tooset up hello OMS dashboard.</span></span> <span data-ttu-id="6e5f1-126">Var olan iki yolu toodo bu: OMS portalında veya Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-126">There are two ways toodo this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="6e5f1-127">OMS portalı</span><span class="sxs-lookup"><span data-stu-id="6e5f1-127">OMS Portal</span></span> 

<span data-ttu-id="6e5f1-128">Toohello OMS portalında oturum (<https://mms.microsoft.com>) ve Git toohello **çözüm Galerisi**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-128">Log in toohello OMS portal (<https://mms.microsoft.com>) and go toohello **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="6e5f1-129">Hello olduğunuzda **çözüm Galerisi**seçin **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-129">Once you are in hello **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="6e5f1-130">Merhaba kapsayıcı çözüm seçtikten sonra hello OMS Genel Bakış Panosu sayfasında döşeme hello görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-130">Once you’ve selected hello Container Solution, you will see hello tile on hello OMS Overview Dashboard page.</span></span> <span data-ttu-id="6e5f1-131">Alınan hello kapsayıcı verileri dizini oluşturulduktan sonra göreceğiniz hello döşeme çözüm görünümü döşeme hakkında bilgi ile doldurulur.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-131">Once hello ingested container data is indexed, you will see hello tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="6e5f1-132">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6e5f1-132">Azure Portal</span></span> 

<span data-ttu-id="6e5f1-133">Oturum açma tooAzure portalında <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-133">Login tooAzure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="6e5f1-134">Git **Market**seçin **izleme + Yönetim** tıklatıp **bkz tüm**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="6e5f1-135">Yazın `containers` arama.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-135">Then Type `containers` in search.</span></span> <span data-ttu-id="6e5f1-136">"Kapsayıcıları" Merhaba arama sonuçlarında görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-136">You will see "containers" in hello search results.</span></span> <span data-ttu-id="6e5f1-137">Seçin **kapsayıcıları** tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="6e5f1-138">Tıkladığınızda **oluşturma**, onu için çalışma alanınızda sorar.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="6e5f1-139">Çalışma alanınızı seçin veya bir yoksa yeni bir çalışma alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="6e5f1-140">Çalışma alanınızı seçtikten sonra tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="6e5f1-141">Merhaba OMS kapsayıcı çözüm hakkında daha fazla bilgi için lütfen toothe bakın [kapsayıcı çözüm günlük analizi](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="6e5f1-141">For more information about hello OMS Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a><span data-ttu-id="6e5f1-142">Nasıl tooscale OMS Aracısı ACS DC/OS ile</span><span class="sxs-lookup"><span data-stu-id="6e5f1-142">How tooscale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="6e5f1-143">Yüklü toohave OMS Aracısı hello gerçek düğüm sayısı yetersiz gerekir ya da daha fazla VM ekleyerek VMSS ölçekleme durumda hello ölçeklendirme tarafından yapabilirsiniz `msoms` hizmet.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-143">In case you need toohave installed OMS agent short of hello actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling hello `msoms` service.</span></span>

<span data-ttu-id="6e5f1-144">TooMarathon veya hello DC/OS kullanıcı Arabirimi Hizmetleri sekmesine gidin ve düğüm sayınız ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-144">You can either go tooMarathon or hello DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="6e5f1-145">Bu hello OMS Aracısı henüz dağıtmadıysanız tooother düğümler dağıtır.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-145">This will deploy tooother nodes which have not yet deployed hello OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="6e5f1-146">MS OMS kaldırma</span><span class="sxs-lookup"><span data-stu-id="6e5f1-146">Uninstall MS OMS</span></span>

<span data-ttu-id="6e5f1-147">toouninstall MS OMS hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="6e5f1-147">toouninstall MS OMS enter hello following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="6e5f1-148">Bize bildirin!!!</span><span class="sxs-lookup"><span data-stu-id="6e5f1-148">Let us know!!!</span></span>
<span data-ttu-id="6e5f1-149">Neler çalışır?</span><span class="sxs-lookup"><span data-stu-id="6e5f1-149">What works?</span></span> <span data-ttu-id="6e5f1-150">Eksik nedir?</span><span class="sxs-lookup"><span data-stu-id="6e5f1-150">What is missing?</span></span> <span data-ttu-id="6e5f1-151">Başka ne için bu toobe sizin için yararlı ihtiyacınız var?</span><span class="sxs-lookup"><span data-stu-id="6e5f1-151">What else do you need for this toobe useful for you?</span></span> <span data-ttu-id="6e5f1-152">Konumundaki bize bildirin <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e5f1-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6e5f1-153">Next steps</span></span>

 <span data-ttu-id="6e5f1-154">Kapsayıcılarınızı, OMS toomonitor ayarladığınız göre[kapsayıcı panonuz bkz](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="6e5f1-154">Now that you have set up OMS toomonitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
