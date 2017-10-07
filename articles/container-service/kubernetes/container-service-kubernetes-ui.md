---
title: "aaaManage Azure Kubernetes web kullanıcı Arabirimi ile küme | Microsoft Docs"
description: "Hello kullanarak Azure kapsayıcı hizmeti kullanıcı Arabiriminde Kubernetes web"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="78e62-103">Kubernetes web kullanıcı Arabirimi Azure kapsayıcı hizmeti ile Merhaba kullanma</span><span class="sxs-lookup"><span data-stu-id="78e62-103">Using hello Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78e62-104">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="78e62-104">Prerequisites</span></span>
<span data-ttu-id="78e62-105">Bu kılavuz, sahibi olduğunuzu varsayar [Azure kapsayıcı hizmeti kullanarak Kubernetes küme oluşturulan](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="78e62-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="78e62-106">Ayrıca, hello Azure CLI 2.0 sahibi olduğunuzu varsayar ve `kubectl` araçları yüklü.</span><span class="sxs-lookup"><span data-stu-id="78e62-106">It also assumes that you have hello Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="78e62-107">Merhaba varsa test edebilirsiniz `az` çalıştırarak yüklü aracı:</span><span class="sxs-lookup"><span data-stu-id="78e62-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="78e62-108">Merhaba yoksa `az` yüklü, aracı yönergeler vardır [burada](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="78e62-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="78e62-109">Merhaba varsa test edebilirsiniz `kubectl` çalıştırarak yüklü aracı:</span><span class="sxs-lookup"><span data-stu-id="78e62-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="78e62-110">Sahip değilseniz `kubectl` yüklü çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="78e62-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="78e62-111">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="78e62-111">Overview</span></span>

### <a name="connect-toohello-web-ui"></a><span data-ttu-id="78e62-112">Toohello web kullanıcı Arabirimi Bağlan</span><span class="sxs-lookup"><span data-stu-id="78e62-112">Connect toohello web UI</span></span>
<span data-ttu-id="78e62-113">Merhaba Kubernetes web kullanıcı arabirimini çalıştırarak başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="78e62-113">You can launch hello Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="78e62-114">Bu, yerel makine toohello Kubernetes web kullanıcı Arabirimi bağlanan bir web tarayıcı yapılandırılmış tootalk tooa güvenli proxy açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="78e62-114">This should open a web browser configured tootalk tooa secure proxy connecting your local machine toohello Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="78e62-115">Oluşturma ve bir hizmet kullanıma sunma</span><span class="sxs-lookup"><span data-stu-id="78e62-115">Create and expose a service</span></span>
1. <span data-ttu-id="78e62-116">Merhaba Kubernetes web kullanıcı Arabirimi,'ı **oluşturma** hello üst sağ penceresinde düğmesini.</span><span class="sxs-lookup"><span data-stu-id="78e62-116">In hello Kubernetes web UI, click **Create** button in hello upper right window.</span></span>

    ![Kubernetes kullanıcı Arabirimi oluşturma](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="78e62-118">Uygulamanızı oluşturma başlayabileceğiniz bir iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="78e62-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="78e62-119">Merhaba ad verin `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="78e62-119">Give it hello name `hello-nginx`.</span></span> <span data-ttu-id="78e62-120">Kullanım hello [ `nginx` Docker kapsayıcıdan](https://hub.docker.com/_/nginx/) ve bu web Hizmeti'nin, üç çoğaltmaları dağıtın.</span><span class="sxs-lookup"><span data-stu-id="78e62-120">Use hello [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Kubernetes Pod Oluştur iletişim kutusu](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="78e62-122">Altında **hizmet**seçin **dış** ve 80 numaralı bağlantı noktasını girin.</span><span class="sxs-lookup"><span data-stu-id="78e62-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="78e62-123">Bu ayar yük-trafik toohello üç çoğaltmaları dengeler.</span><span class="sxs-lookup"><span data-stu-id="78e62-123">This setting load-balances traffic toohello three replicas.</span></span>

    ![Kubernetes hizmeti oluşturma iletişim kutusu](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="78e62-125">Tıklatın **dağıtma** toodeploy Bu kapsayıcılar ve Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="78e62-125">Click **Deploy** toodeploy these containers and services.</span></span>

    ![Kubernetes dağıtma](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="78e62-127">Kapsayıcılarınızı görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="78e62-127">View your containers</span></span>
<span data-ttu-id="78e62-128">Tıklattıktan sonra **dağıtma**, hello UI dağıttığı gibi hizmetiniz bir görünümünü gösterir:</span><span class="sxs-lookup"><span data-stu-id="78e62-128">After you click **Deploy**, hello UI shows a view of your service as it deploys:</span></span>

![Kubernetes durumu](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="78e62-130">Merhaba sol tarafında, UI altında her hello daire Kubernetes nesnesinde hello durumunu görebilirsiniz **pod'ları**.</span><span class="sxs-lookup"><span data-stu-id="78e62-130">You can see hello status of each Kubernetes object in hello circle on hello left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="78e62-131">Kısmen dolu daire ise, ardından hello nesne hala dağıtıyor.</span><span class="sxs-lookup"><span data-stu-id="78e62-131">If it is a partially full circle, then hello object is still deploying.</span></span> <span data-ttu-id="78e62-132">Bir nesne tam olarak dağıtıldığında, yeşil bir onay işareti görüntüler:</span><span class="sxs-lookup"><span data-stu-id="78e62-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Dağıtılan Kubernetes](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="78e62-134">Her şeyi çalışmaya başladıktan sonra web hizmeti çalıştıran hello pod'ları toosee ayrıntılarını birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="78e62-134">Once everything is running, click one of your pods toosee details about hello running web service.</span></span>

![Kubernetes pod'ları](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="78e62-136">Merhaba, **pod'ları** görünümü Merhaba kapsayıcılara hello pod yanı sıra bu kapsayıcıları tarafından kullanılan hello CPU ve bellek kaynakları hakkında bilgileri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="78e62-136">In hello **Pods** view, you can see information about hello containers in hello pod as well as hello CPU and memory resources used by those containers:</span></span>

![Kubernetes kaynakları](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="78e62-138">Merhaba kaynakları görmüyorsanız, toowait veri toopropagate izleme hello için birkaç dakika gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="78e62-138">If you don't see hello resources, you may need toowait a few minutes for hello monitoring data toopropagate.</span></span>

<span data-ttu-id="78e62-139">toosee hello günlükleri, kapsayıcı için tıklatın **görüntülemek günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="78e62-139">toosee hello logs for your container, click **View logs**.</span></span>

![Kubernetes günlükleri](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="78e62-141">Hizmetinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="78e62-141">Viewing your service</span></span>
<span data-ttu-id="78e62-142">Bir dış toplama toorunning, kapsayıcıları hello Kubernetes UI oluşturdu `Service` bir yük dengeleyici toobring trafiği toohello kapsayıcıları kümenizdeki sağlar.</span><span class="sxs-lookup"><span data-stu-id="78e62-142">In addition toorunning your containers, hello Kubernetes UI has created an external `Service` which provisions a load balancer toobring traffic toohello containers in your cluster.</span></span>

<span data-ttu-id="78e62-143">Merhaba sol gezinti bölmesinde **Hizmetleri** tooview tüm hizmetleri (olması gerektiğini tek).</span><span class="sxs-lookup"><span data-stu-id="78e62-143">In hello left navigation pane, click **Services** tooview all services (there should be only one).</span></span>

![Kubernetes Hizmetleri](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="78e62-145">Bu görünümde tooyour hizmet ayrılmış bir dış uç noktası (IP adresi) görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="78e62-145">In that view, you should see an external endpoint (IP address) that has been allocated tooyour service.</span></span>
<span data-ttu-id="78e62-146">Bu IP adresi tıklarsanız, yük dengeleyicinin ardında çalışan, Nginx kapsayıcısı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="78e62-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![nginx görünümü](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="78e62-148">Hizmetinizi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="78e62-148">Resizing your service</span></span>
<span data-ttu-id="78e62-149">Toplama tooviewing, nesnelerinizi UI Merhaba, düzenleme ve hello Kubernetes API nesneleri güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="78e62-149">In addition tooviewing your objects in hello UI, you can edit and update hello Kubernetes API objects.</span></span>

<span data-ttu-id="78e62-150">Önce tıklatın **dağıtımları** sol gezinti bölmesinde toosee hello dağıtım hizmetiniz için hello içinde.</span><span class="sxs-lookup"><span data-stu-id="78e62-150">First, click **Deployments** in hello left navigation pane toosee hello deployment for your service.</span></span>

<span data-ttu-id="78e62-151">Bu görünümde olduktan sonra hello çoğaltma kümesinde tıklayın ve ardından **Düzenle** hello üst gezinti çubuğunda:</span><span class="sxs-lookup"><span data-stu-id="78e62-151">Once you are in that view, click on hello replica set, and then click **Edit** in hello upper navigation bar:</span></span>

![Kubernetes Düzenle](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="78e62-153">Merhaba Düzenle `spec.replicas` alan toobe `2`, tıklatıp **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="78e62-153">Edit hello `spec.replicas` field toobe `2`, and click **Update**.</span></span>

<span data-ttu-id="78e62-154">Bu, çoğaltmaları toodrop tootwo hello sayısı, pod'ları birini silerek neden olur.</span><span class="sxs-lookup"><span data-stu-id="78e62-154">This causes hello number of replicas toodrop tootwo by deleting one of your pods.</span></span>

 

