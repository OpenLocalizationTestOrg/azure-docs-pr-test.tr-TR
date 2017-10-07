---
title: "aaaAzure kapsayıcı örnekleri ve kapsayıcı düzenleme"
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
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="38a1d-103">Azure kapsayıcı örnekleri ve kapsayıcı orchestrators</span><span class="sxs-lookup"><span data-stu-id="38a1d-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="38a1d-104">Kendi küçük boyutu ve uygulama yönlendirme nedeniyle kapsayıcıları Çevik teslim ortamları ve mikro hizmet tabanlı mimariler için uygundur.</span><span class="sxs-lookup"><span data-stu-id="38a1d-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="38a1d-105">Başlangıç görevini otomatikleştirmek ve çok sayıda kapsayıcıları ve nasıl etkileşim kurduklarını yönetme olarak bilinir *orchestration*.</span><span class="sxs-lookup"><span data-stu-id="38a1d-105">hello task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="38a1d-106">Popüler kapsayıcı orchestrators dahil Kubernetes, DC/OS ve tümü hello kullanılabilir Docker Swarm, [Azure kapsayıcı hizmeti](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="38a1d-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="38a1d-107">Bazı zamanlama özellikleri orchestration platformlarının temel hello Azure kapsayıcı örnekleri sağlar, ancak bu platformlar sağlar ve hatta bunları tamamlayıcı olabilir hello yüksek değerli hizmetleri kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="38a1d-107">Azure Container Instances provides some of hello basic scheduling capabilities of orchestration platforms, but it does not cover hello higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="38a1d-108">Bu makalede hello kapsamını ne Azure kapsayıcı örnekleri işler ve kapsayıcı orchestrators ile nasıl tam etkileşebilir açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="38a1d-108">This article describes hello scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="38a1d-109">Geleneksel düzenleme</span><span class="sxs-lookup"><span data-stu-id="38a1d-109">Traditional orchestration</span></span>

<span data-ttu-id="38a1d-110">orchestration standart tanımını Hello hello aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="38a1d-110">hello standard definition of orchestration includes hello following tasks:</span></span>

- <span data-ttu-id="38a1d-111">**Zamanlama**: verilen bir kapsayıcı görüntüsü ve bir kaynak isteği, hangi toorun hello kapsayıcısı üzerinde uygun bir makine bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="38a1d-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which toorun hello container.</span></span>
- <span data-ttu-id="38a1d-112">**Benzeşim/Anti-affinity**: kapsayıcıları bir dizi diğer (performans için) yakındaki veya yeterince kadar parçalayın (kullanılabilirlik için) çalışması gerektiğini belirtmek.</span><span class="sxs-lookup"><span data-stu-id="38a1d-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="38a1d-113">**Sistem durumu izleme**: kapsayıcı hatalarını ve otomatik olarak izlemek yeniden zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38a1d-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="38a1d-114">**Yük devretme**: her makinede çalışan izlemek ve başarısız makineler toohealthy düğümleri kapsayıcılardan yeniden zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="38a1d-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines toohealthy nodes.</span></span>
- <span data-ttu-id="38a1d-115">**Ölçeklendirme**: ekleyin veya kapsayıcı örnekleri toomatch isteğe bağlı, el ile veya otomatik olarak kaldırın.</span><span class="sxs-lookup"><span data-stu-id="38a1d-115">**Scaling**: Add or remove container instances toomatch demand, either manually or automatically.</span></span>
- <span data-ttu-id="38a1d-116">**Ağ**: birden çok ana bilgisayar makine genelinde kapsayıcıları toocommunicate düzenlemekten bir katman ağ sağlar.</span><span class="sxs-lookup"><span data-stu-id="38a1d-116">**Networking**: Provide an overlay network for coordinating containers toocommunicate across multiple host machines.</span></span>
- <span data-ttu-id="38a1d-117">**Hizmet bulma**: ana makineler arasında taşımak ve IP adreslerini değiştirmek gibi bile kapsayıcıları toolocate birbirine otomatik olarak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="38a1d-117">**Service discovery**: Enable containers toolocate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="38a1d-118">**Uygulama yükseltme Eşgüdümlü**: kapsayıcı yükseltmeler tooavoid uygulama kesinti yönetebilir ve bir sorun yaşanırsa geri alma etkinleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="38a1d-118">**Coordinated application upgrades**: Manage container upgrades tooavoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="38a1d-119">Azure kapsayıcı örnekleri düzenlemesini: bir katmanlı yaklaşımın</span><span class="sxs-lookup"><span data-stu-id="38a1d-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="38a1d-120">Tüm hello zamanlama sağlayan bir katmanlı yaklaşımın tooorchestration Azure kapsayıcı örnekleri sağlar ve yönetim özellikleri, orchestrator platformları toomanage çok kapsayıcı görevler, en üstünde olanak tanırken, tek bir kapsayıcı toorun gerekli.</span><span class="sxs-lookup"><span data-stu-id="38a1d-120">Azure Container Instances enables a layered approach tooorchestration, providing all of hello scheduling and management capabilities required toorun a single container, while allowing orchestrator platforms toomanage multi-container tasks on top of it.</span></span>

<span data-ttu-id="38a1d-121">Azure tarafından tüm altyapı kapsayıcı örnekleri için temel alınan hello yönetilir çünkü bir orchestrator platformu hangi toorun uygun ana makinede tek bir kapsayıcı bulma ile tooconcern kendisini gerekmez.</span><span class="sxs-lookup"><span data-stu-id="38a1d-121">Because all of hello underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need tooconcern itself with finding an appropriate host machine on which toorun a single container.</span></span> <span data-ttu-id="38a1d-122">bir her zaman kullanılabilir hello bulutun Hello esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="38a1d-122">hello elasticity of hello cloud ensures that one is always available.</span></span> <span data-ttu-id="38a1d-123">Bunun yerine, hello orchestrator hello geliştirilmesini ölçeklendirme dahil olmak üzere birden çok kapsayıcı mimarileri ve Eşgüdümlü yükseltmeleri basitleştirmek hello görevlerde odaklanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38a1d-123">Instead, hello orchestrator can focus on hello tasks that simplify hello development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="38a1d-124">Olası senaryolar</span><span class="sxs-lookup"><span data-stu-id="38a1d-124">Potential scenarios</span></span>

<span data-ttu-id="38a1d-125">Azure kapsayıcı örnekleri ile orchestrator tümleştirme hala nascent olsa da, birkaç farklı ortamlarda ortaya çıkan düşündüğünüz:</span><span class="sxs-lookup"><span data-stu-id="38a1d-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="38a1d-126">Orchestration kapsayıcı örneklerinin özel olarak</span><span class="sxs-lookup"><span data-stu-id="38a1d-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="38a1d-127">Hızlı Başlat ve fatura hello tarafından ikinci, özel olarak üzerinde bağlı bir ortam Azure kapsayıcı örnekleri sunar hello en hızlı yolu tooget başlatıldı ve yüksek oranda değişken iş yükleri ile toodeal.</span><span class="sxs-lookup"><span data-stu-id="38a1d-127">Because they start quickly and bill by hello second, an environment based exclusively on Azure Container Instances offers hello fastest way tooget started and toodeal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="38a1d-128">Kapsayıcı örnekleri ve sanal makineleri kapsayıcılarında birleşimi</span><span class="sxs-lookup"><span data-stu-id="38a1d-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="38a1d-129">Uzun süre çalışan için ayrılmış sanal makine bir kümede kapsayıcıları yönetme kararlı iş yükleri, genellikle hello aynı kapsayıcı örnekleriyle çalışan kapsayıcılar daha ucuz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="38a1d-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running hello same containers with Container Instances.</span></span> <span data-ttu-id="38a1d-130">Ancak, kapsayıcı örnekleri hızlı bir şekilde genişletme ve beklenmeyen veya kısa süreli ani kullanımı ile genel kapasitesini toodeal daraltılırken için harika bir çözüm sunar.</span><span class="sxs-lookup"><span data-stu-id="38a1d-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity toodeal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="38a1d-131">Sanal makine kümenizdeki hello sayısı ölçeğini, yerine daha sonra bu makinelere ek kapsayıcıları dağıtma, hello orchestrator yalnızca hello ek kapsayıcıları kapsayıcı örnekleri kullanılarak zamanlayabilir ve bunlar olduğunuzda silin yok artık gerekli.</span><span class="sxs-lookup"><span data-stu-id="38a1d-131">Rather than scaling out hello number of virtual machines in your cluster, then deploying additional containers onto those machines, hello orchestrator can simply schedule hello additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="38a1d-132">Örnek uygulama: Kubernetes için Azure kapsayıcı örnekleri Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="38a1d-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="38a1d-133">nasıl kapsayıcı orchestration platformları tümleştirebilir Azure kapsayıcı örnekleriyle toodemonstrate, biz başlatıldı yapı bir [Kubernetes için örnek Bağlayıcısı][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="38a1d-133">toodemonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="38a1d-134">Merhaba Kubernetes taklit için bağlayıcı hello [kubelet] [ kubelet-doc] sınırsız kapasiteye sahip bir düğüm olarak kaydetme ve hello oluşturulmasını göndermeyi [pod'ları] [ pod-doc] Azure kapsayıcı durumlarda kapsayıcı grupları olarak.</span><span class="sxs-lookup"><span data-stu-id="38a1d-134">hello connector for Kubernetes mimics hello [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching hello creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="38a1d-135">Diğer orchestrators bağlayıcılarının platform temelleri toocombine hello güç hello orchestrator API'si hello hızı ile ve Azure kapsayıcı örnekleri kapsayıcılarında yönetme Basitlik ile benzer şekilde tümleşik oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="38a1d-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives toocombine hello power of hello orchestrator API with hello speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="38a1d-136">Kubernetes için ACI bağlayıcı hello *Deneysel* ve üretimde kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="38a1d-136">hello ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38a1d-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38a1d-137">Next steps</span></span>

<span data-ttu-id="38a1d-138">İlk kapsayıcı hello kullanarak Azure kapsayıcı örnekleri ile oluşturmak [Hızlı Başlangıç Kılavuzu](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="38a1d-138">Create your first container with Azure Container Instances using hello [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/