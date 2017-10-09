---
title: "aaaMonitor Azure Kubernetes küme ile Datadog | Microsoft Docs"
description: "Kubernetes Datadog kullanarak Azure kapsayıcı hizmeti kümesinde izleme"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="ced7e-103">Azure kapsayıcı hizmeti kümesi DataDog ile izleme</span><span class="sxs-lookup"><span data-stu-id="ced7e-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ced7e-104">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ced7e-104">Prerequisites</span></span>
<span data-ttu-id="ced7e-105">Bu kılavuz, sahibi olduğunuzu varsayar [Azure kapsayıcı hizmeti kullanarak Kubernetes küme oluşturulan](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="ced7e-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="ced7e-106">Ayrıca, hello sahibi olduğunuzu varsayar `az` Azure CLI ve `kubectl` araçları yüklü.</span><span class="sxs-lookup"><span data-stu-id="ced7e-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="ced7e-107">Merhaba varsa test edebilirsiniz `az` çalıştırarak yüklü aracı:</span><span class="sxs-lookup"><span data-stu-id="ced7e-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="ced7e-108">Merhaba yoksa `az` yüklü, aracı yönergeler vardır [burada](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="ced7e-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="ced7e-109">Merhaba varsa test edebilirsiniz `kubectl` çalıştırarak yüklü aracı:</span><span class="sxs-lookup"><span data-stu-id="ced7e-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="ced7e-110">Sahip değilseniz `kubectl` yüklü çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ced7e-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="ced7e-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="ced7e-111">DataDog</span></span>
<span data-ttu-id="ced7e-112">Datadog, Azure kapsayıcı hizmeti kümesi kapsayıcılara gelen izleme verilerini toplayan izleme bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="ced7e-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="ced7e-113">Datadog Docker tümleştirmesi, kapsayıcılara belirli ölçümleri görebileceğiniz bir Pano vardır.</span><span class="sxs-lookup"><span data-stu-id="ced7e-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="ced7e-114">Kapsayıcılardan toplanan ölçümleri CPU, bellek, ağ ve g/ç tarafından düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="ced7e-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="ced7e-115">Datadog ölçümleri kapsayıcıları ve görüntüleri halinde ayırır.</span><span class="sxs-lookup"><span data-stu-id="ced7e-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="ced7e-116">İlk çok gereksinim[bir hesap oluşturun](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="ced7e-116">You first need too[create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a><span data-ttu-id="ced7e-117">DaemonSet ile Merhaba Datadog aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="ced7e-117">Installing hello Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="ced7e-118">DaemonSets Kubernetes toorun tarafından kullanılan bir kapsayıcı hello kümedeki her ana bilgisayarda tek bir örneği.</span><span class="sxs-lookup"><span data-stu-id="ced7e-118">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="ced7e-119">Bunlar izleme aracıları çalıştırmak için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="ced7e-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="ced7e-120">Datadog oturum açtıktan sonra hello izleyebilirsiniz [Datadog yönergeleri](https://app.datadoghq.com/account/settings#agent/kubernetes) bir DaemonSet kullanarak kümenizde tooinstall Datadog aracıları.</span><span class="sxs-lookup"><span data-stu-id="ced7e-120">Once you have logged into Datadog, you can follow hello [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ced7e-121">Sonuç</span><span class="sxs-lookup"><span data-stu-id="ced7e-121">Conclusion</span></span>
<span data-ttu-id="ced7e-122">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="ced7e-122">That's it!</span></span> <span data-ttu-id="ced7e-123">Bir kez hello aracıları ayarlama ve çalıştırdığınız hello konsol verilerde birkaç dakika içinde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ced7e-123">Once hello agents are up and running you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="ced7e-124">Tümleşik hello ziyaret ettiğiniz [kubernetes Pano](https://app.datadoghq.com/screen/integration/kubernetes) toosee kümenizi özetini.</span><span class="sxs-lookup"><span data-stu-id="ced7e-124">You can visit hello integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee a summary of your cluster.</span></span>
