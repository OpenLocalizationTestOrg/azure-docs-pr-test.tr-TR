---
title: "aaaMonitor Azure Kubernetes küme - Sysdig | Microsoft Docs"
description: "Kubernetes Sysdig kullanarak Azure kapsayıcı hizmeti kümesinde izleme"
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="f4e1c-103">Sysdig kullanarak Azure kapsayıcı hizmeti Kubernetes küme izleme</span><span class="sxs-lookup"><span data-stu-id="f4e1c-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4e1c-104">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f4e1c-104">Prerequisites</span></span>
<span data-ttu-id="f4e1c-105">Bu kılavuz, sahibi olduğunuzu varsayar [Azure kapsayıcı hizmeti kullanarak Kubernetes küme oluşturulan](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="f4e1c-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="f4e1c-106">Hello azure CLI ve kubectl araçlarının yüklü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="f4e1c-106">It also assumes that you have hello azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="f4e1c-107">Merhaba varsa test edebilirsiniz `az` çalıştırarak yüklü aracı:</span><span class="sxs-lookup"><span data-stu-id="f4e1c-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="f4e1c-108">Merhaba yoksa `az` yüklü, aracı yönergeler vardır [burada](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="f4e1c-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="f4e1c-109">Merhaba varsa test edebilirsiniz `kubectl` çalıştırarak yüklü aracı:</span><span class="sxs-lookup"><span data-stu-id="f4e1c-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="f4e1c-110">Sahip değilseniz `kubectl` yüklü çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f4e1c-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="f4e1c-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="f4e1c-111">Sysdig</span></span>
<span data-ttu-id="f4e1c-112">Bir dış Azure'da çalışan Kubernetes kümenizi kapsayıcılarında izleyebilirsiniz bir hizmet şirket olarak izleme Sysdig olur.</span><span class="sxs-lookup"><span data-stu-id="f4e1c-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="f4e1c-113">Sysdig kullanarak etkin bir Sysdig hesabı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f4e1c-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="f4e1c-114">İçin bir hesap üzerinde kaydolabilirsiniz kendi [site](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="f4e1c-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="f4e1c-115">Toohello Sysdig bulut Web sitesinde oturum açtınız sonra kullanıcı adına tıklayın ve hello sayfasında "Erişim anahtarınızı." görmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="f4e1c-115">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Sysdig API anahtarı](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a><span data-ttu-id="f4e1c-117">Merhaba Sysdig aracıları tooKubernetes yükleme</span><span class="sxs-lookup"><span data-stu-id="f4e1c-117">Installing hello Sysdig agents tooKubernetes</span></span>
<span data-ttu-id="f4e1c-118">Her bir işlemi Sysdig çalışır kapsayıcılarınızı makine bir Kubernetes kullanarak toomonitor `DaemonSet`.</span><span class="sxs-lookup"><span data-stu-id="f4e1c-118">toomonitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="f4e1c-119">DaemonSets bir kapsayıcı makine başına tek bir örneğini çalıştıran Kubernetes API nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="f4e1c-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="f4e1c-120">Bunlar Sysdig'ın İzleme Aracısı hello gibi araçlar yüklemek için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="f4e1c-120">They're perfect for installing tools like hello Sysdig's monitoring agent.</span></span>

<span data-ttu-id="f4e1c-121">tooinstall hello Sysdig daemonset ilk karşıdan [hello şablonu](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) sysdig gelen.</span><span class="sxs-lookup"><span data-stu-id="f4e1c-121">tooinstall hello Sysdig daemonset, you should first download [hello template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="f4e1c-122">Bu dosya olarak kaydetmek `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="f4e1c-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="f4e1c-123">Linux ve OS X çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f4e1c-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="f4e1c-124">PowerShell içinde:</span><span class="sxs-lookup"><span data-stu-id="f4e1c-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="f4e1c-125">Ardından bu dosya tooinsert erişim Sysdig hesabınızdan aldığınız anahtarınız, düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="f4e1c-125">Next edit that file tooinsert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="f4e1c-126">Son olarak, hello DaemonSet oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f4e1c-126">Finally, create hello DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="f4e1c-127">İzlemenizi görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="f4e1c-127">View your monitoring</span></span>
<span data-ttu-id="f4e1c-128">Yüklü ve çalışır sonra hello aracıları veri geri tooSysdig pompa.</span><span class="sxs-lookup"><span data-stu-id="f4e1c-128">Once installed and running, hello agents should pump data back tooSysdig.</span></span>  <span data-ttu-id="f4e1c-129">Toothe dönün [sysdig Pano](https://app.sysdigcloud.com) ve kapsayıcıları hakkında bilgiler görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4e1c-129">Go back toothe [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="f4e1c-130">Kubernetes özel panolar aracılığıyla da yükleyebilirsiniz [yeni pano Sihirbazı'nı](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="f4e1c-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
