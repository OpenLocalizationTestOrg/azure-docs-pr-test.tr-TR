---
title: "Azure kapsayıcı örnekleri ve kapsayıcı düzenleme"
description: "Azure kapsayıcı örnekleri kapsayıcı orchestrators ile nasıl etkileşim anlama"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: cbb558a92d565759c8dc7d2693960955eb053b0a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="0816a-103">Azure kapsayıcı örnekleri ve kapsayıcı orchestrators</span><span class="sxs-lookup"><span data-stu-id="0816a-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="0816a-104">Kendi küçük boyutu ve uygulama yönlendirme nedeniyle kapsayıcıları Çevik teslim ortamları ve mikro hizmet tabanlı mimariler için uygundur.</span><span class="sxs-lookup"><span data-stu-id="0816a-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="0816a-105">Otomatikleştirme ve çok sayıda kapsayıcıları ve nasıl etkileşim kurduklarını yönetme görevini olarak bilinen *orchestration*.</span><span class="sxs-lookup"><span data-stu-id="0816a-105">The task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="0816a-106">Popüler kapsayıcı orchestrators dahil Kubernetes, DC/OS ve tümü kullanılabilir Docker Swarm, [Azure kapsayıcı hizmeti](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="0816a-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in the [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="0816a-107">Azure kapsayıcı örnekleri bazı orchestration platformları temel zamanlama özelliklerini sağlar, ancak bu platformlar sağlar ve hatta bunları tamamlayıcı olabilir daha yüksek değerli hizmetleri kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="0816a-107">Azure Container Instances provides some of the basic scheduling capabilities of orchestration platforms, but it does not cover the higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="0816a-108">Bu makalede, Azure kapsayıcı örnekleri ne işler ve kapsayıcı orchestrators ile nasıl tam etkileşebilir kapsamını açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0816a-108">This article describes the scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="0816a-109">Geleneksel düzenleme</span><span class="sxs-lookup"><span data-stu-id="0816a-109">Traditional orchestration</span></span>

<span data-ttu-id="0816a-110">Orchestration standart tanımını aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="0816a-110">The standard definition of orchestration includes the following tasks:</span></span>

- <span data-ttu-id="0816a-111">**Zamanlama**: verilen bir kapsayıcı görüntüsü ve bir kaynak isteği, kapsayıcı çalıştırmak için uygun bir makine bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="0816a-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which to run the container.</span></span>
- <span data-ttu-id="0816a-112">**Benzeşim/Anti-affinity**: kapsayıcıları bir dizi diğer (performans için) yakındaki veya yeterince kadar parçalayın (kullanılabilirlik için) çalışması gerektiğini belirtmek.</span><span class="sxs-lookup"><span data-stu-id="0816a-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="0816a-113">**Sistem durumu izleme**: kapsayıcı hatalarını ve otomatik olarak izlemek yeniden zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0816a-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="0816a-114">**Yük devretme**: her makinede çalışan izlemek ve başarısız makineler kapsayıcılardan sağlıklı düğümlere yeniden zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="0816a-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines to healthy nodes.</span></span>
- <span data-ttu-id="0816a-115">**Ölçeklendirme**: isteğe bağlı, el ile veya otomatik olarak eşleştirmek için kapsayıcı örnekler ekleyip kaldıracaktır.</span><span class="sxs-lookup"><span data-stu-id="0816a-115">**Scaling**: Add or remove container instances to match demand, either manually or automatically.</span></span>
- <span data-ttu-id="0816a-116">**Ağ**: birden çok ana makine arasında iletişim kurmak için kapsayıcıları düzenlemekten bir katman ağ sağlar.</span><span class="sxs-lookup"><span data-stu-id="0816a-116">**Networking**: Provide an overlay network for coordinating containers to communicate across multiple host machines.</span></span>
- <span data-ttu-id="0816a-117">**Hizmet bulma**: etkinleştirmek ana makineler arasında taşımak ve IP adreslerini değiştirmek gibi bile birbirlerine otomatik olarak bulmak kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="0816a-117">**Service discovery**: Enable containers to locate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="0816a-118">**Uygulama yükseltme Eşgüdümlü**: uygulama kesinti önlemek ve bir sorun yaşanırsa geri alma etkinleştirmek için kapsayıcı yükseltmelerini yönetme.</span><span class="sxs-lookup"><span data-stu-id="0816a-118">**Coordinated application upgrades**: Manage container upgrades to avoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="0816a-119">Azure kapsayıcı örnekleri düzenlemesini: bir katmanlı yaklaşımın</span><span class="sxs-lookup"><span data-stu-id="0816a-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="0816a-120">Azure kapsayıcı örnekleri, tüm orchestrator platformlar, üzerinde birden çok kapsayıcı görevleri yönetmek üzere izin verirken tek bir kapsayıcı çalıştırmak için gerekli planlama ve yönetim özellikleri sağlayarak orchestration, katmanlı bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="0816a-120">Azure Container Instances enables a layered approach to orchestration, providing all of the scheduling and management capabilities required to run a single container, while allowing orchestrator platforms to manage multi-container tasks on top of it.</span></span>

<span data-ttu-id="0816a-121">Azure tarafından tüm altyapının kapsayıcı örnekleri için yönetilen çünkü bir orchestrator platformu kendisini bir uygun konak makinesi üzerinde tek bir kapsayıcı çalıştırmak için bulma ile ilgili gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0816a-121">Because all of the underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need to concern itself with finding an appropriate host machine on which to run a single container.</span></span> <span data-ttu-id="0816a-122">Bir her zaman kullanılabilir bulut esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="0816a-122">The elasticity of the cloud ensures that one is always available.</span></span> <span data-ttu-id="0816a-123">Bunun yerine, orchestrator ölçeklendirme dahil olmak üzere birden çok kapsayıcı mimarileri ve Eşgüdümlü yükseltmeleri geliştirilmesini basitleştirmek görevlerde odaklanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0816a-123">Instead, the orchestrator can focus on the tasks that simplify the development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="0816a-124">Olası senaryolar</span><span class="sxs-lookup"><span data-stu-id="0816a-124">Potential scenarios</span></span>

<span data-ttu-id="0816a-125">Azure kapsayıcı örnekleri ile orchestrator tümleştirme hala nascent olsa da, birkaç farklı ortamlarda ortaya çıkan düşündüğünüz:</span><span class="sxs-lookup"><span data-stu-id="0816a-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="0816a-126">Orchestration kapsayıcı örneklerinin özel olarak</span><span class="sxs-lookup"><span data-stu-id="0816a-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="0816a-127">Hızlı Başlat ve ikinciye faturalandırmak çünkü özel olarak Azure kapsayıcı örneklerinde bağlı bir ortam başlamak ve yüksek oranda değişken iş yükleri ile mücadele etmek için en hızlı yolu sunar.</span><span class="sxs-lookup"><span data-stu-id="0816a-127">Because they start quickly and bill by the second, an environment based exclusively on Azure Container Instances offers the fastest way to get started and to deal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="0816a-128">Kapsayıcı örnekleri ve sanal makineleri kapsayıcılarında birleşimi</span><span class="sxs-lookup"><span data-stu-id="0816a-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="0816a-129">Uzun süre çalışan, kararlı iş yükleri için ayrılmış sanal makine bir kümede kapsayıcıları yönetme genellikle kapsayıcı örnekleriyle aynı kapsayıcıları çalıştıran daha ucuz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0816a-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running the same containers with Container Instances.</span></span> <span data-ttu-id="0816a-130">Ancak, kapsayıcı örnekleri hızlı bir şekilde genişletme ve beklenmeyen veya kısa süreli ani kullanımı uğraşmanız genel kapasitenizi daraltılırken için harika bir çözüm sunar.</span><span class="sxs-lookup"><span data-stu-id="0816a-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity to deal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="0816a-131">Sanal makine kümenizdeki sayısı ölçeğini, yerine daha sonra bu makinelere ek kapsayıcıları dağıtma, orchestrator yalnızca kapsayıcı örnekleri kullanılarak ek kapsayıcıları zamanlayabilir ve artık gerekmediğinde silin.</span><span class="sxs-lookup"><span data-stu-id="0816a-131">Rather than scaling out the number of virtual machines in your cluster, then deploying additional containers onto those machines, the orchestrator can simply schedule the additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="0816a-132">Örnek uygulama: Kubernetes için Azure kapsayıcı örnekleri Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="0816a-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="0816a-133">Kapsayıcı orchestration platformları Azure kapsayıcı örnekleri ile nasıl tümleşebilir göstermek için biz yapı başlattığınız bir [Kubernetes için örnek Bağlayıcısı][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="0816a-133">To demonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="0816a-134">Bağlayıcı Kubernetes için taklit eder [kubelet] [ kubelet-doc] sınırsız kapasiteye sahip bir düğüm olarak kaydetme ve oluşturulmasını göndermeyi [pod'ları] [ pod-doc] Azure kapsayıcı durumlarda kapsayıcı grupları olarak.</span><span class="sxs-lookup"><span data-stu-id="0816a-134">The connector for Kubernetes mimics the [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching the creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="0816a-135">Diğer orchestrators bağlayıcılarının API orchestrator gücünü hızı ve Azure kapsayıcı örnekleri kapsayıcılarında yönetme Basitlik birleştirip platform temelleri ile benzer şekilde tümleşik oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="0816a-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives to combine the power of the orchestrator API with the speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="0816a-136">Kubernetes ACI Bağlayıcısı *Deneysel* ve üretimde kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="0816a-136">The ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0816a-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0816a-137">Next steps</span></span>

<span data-ttu-id="0816a-138">Azure kapsayıcı örneği kullanarak, ilk kapsayıcı oluşturmak [Hızlı Başlangıç Kılavuzu](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="0816a-138">Create your first container with Azure Container Instances using the [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/