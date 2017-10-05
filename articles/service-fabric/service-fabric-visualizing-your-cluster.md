---
title: "Service Fabric Explorer kullanarak kümenizi Görselleştirme | Microsoft Docs"
description: "Service Fabric Explorer inceleme ve bulut uygulamaları ve Microsoft Azure Service Fabric kümesindeki düğümler yönetmek için bir web tabanlı araçtır."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 789793a7f50170188d688881a9178546c3074018
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="e1e7e-103">Service Fabric Explorer ile kümenizi görselleştirme</span><span class="sxs-lookup"><span data-stu-id="e1e7e-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="e1e7e-104">Service Fabric Explorer inceleme ve uygulamaları ve bir Azure Service Fabric kümesindeki düğümler yönetmek için bir web tabanlı araçtır.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="e1e7e-105">Her zaman kümenizi nerede çalıştığına bakmaksızın kullanılabilir olması için Service Fabric Explorer doğrudan küme içinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-105">Service Fabric Explorer is hosted directly within the cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="e1e7e-106">Video öğretici</span><span class="sxs-lookup"><span data-stu-id="e1e7e-106">Video tutorial</span></span>

<span data-ttu-id="e1e7e-107">Service Fabric Explorer kullanmayı öğrenmek için aşağıdaki Microsoft Virtual Academy videoyu izleyin:</span><span class="sxs-lookup"><span data-stu-id="e1e7e-107">To learn how to use Service Fabric Explorer, watch the following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-to-service-fabric-explorer"></a><span data-ttu-id="e1e7e-108">Service Fabric Gezgini'ne Bağlan</span><span class="sxs-lookup"><span data-stu-id="e1e7e-108">Connect to Service Fabric Explorer</span></span>
<span data-ttu-id="e1e7e-109">Yönergeleri izlediyseniz [geliştirme ortamınızı hazırlama](service-fabric-get-started.md), http://localhost: 19080/Explorer giderek yerel kümenizde Service Fabric Explorer başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-109">If you have followed the instructions to [prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating to http://localhost:19080/Explorer.</span></span>

## <a name="understand-the-service-fabric-explorer-layout"></a><span data-ttu-id="e1e7e-110">Service Fabric Explorer düzeni anlama</span><span class="sxs-lookup"><span data-stu-id="e1e7e-110">Understand the Service Fabric Explorer layout</span></span>
<span data-ttu-id="e1e7e-111">Soldaki ağaç kullanarak Service Fabric Explorer gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-111">You can navigate through Service Fabric Explorer by using the tree on the left.</span></span> <span data-ttu-id="e1e7e-112">Ağaç kökünde küme Panosu uygulama ve düğüm durumu özetini dahil olmak üzere kümenizi genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-112">At the root of the tree, the cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Service Fabric Explorer küme Panosu][sfx-cluster-dashboard]

### <a name="view-the-clusters-layout"></a><span data-ttu-id="e1e7e-114">Kümenin düzeni görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="e1e7e-114">View the cluster's layout</span></span>
<span data-ttu-id="e1e7e-115">Bir Service Fabric kümesindeki düğümler hata etki alanı arasında iki boyutlu bir kılavuz yerleştirilir ve etki alanlarını yükseltme.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="e1e7e-116">Bu yerleştirme uygulamalarınızı donanım hataları ve uygulama yükseltmelerini varlığında kullanılabilir kalmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-116">This placement ensures that your applications remain available in the presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="e1e7e-117">Nasıl geçerli Küme Küme eşlemesi kullanarak düzenlendiğini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-117">You can view how the current cluster is laid out by using the cluster map.</span></span>

![Service Fabric Explorer küme eşleme][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="e1e7e-119">Görünüm uygulamaları ve Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="e1e7e-119">View applications and services</span></span>
<span data-ttu-id="e1e7e-120">Küme iki alt ağaçları içerir: biri uygulamaları ve diğer düğümleri için.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-120">The cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="e1e7e-121">Service Fabric'ın mantıksal hiyerarşide gezinmek için uygulama görünümü kullanabilirsiniz: uygulamaları, hizmetleri, bölümler ve çoğaltmalar.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-121">You can use the application view to navigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="e1e7e-122">Uygulama aşağıdaki örnekte **Uygulamam** iki hizmetinden, oluşan **Mystatefulservice'ten** ve **WebService**.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-122">In the example below, the application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="e1e7e-123">Bu yana **Mystatefulservice'ten** durum bilgisi olan bir birincil ve iki ikincil çoğaltma sahip bir bölüm içerir.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="e1e7e-124">Bunun aksine, WebSvcService durum bilgisiz ve tek bir örnek içerir.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Service Fabric Explorer uygulama görünümü][sfx-application-tree]

<span data-ttu-id="e1e7e-126">Her ağacı düzeyinde ana bölmede öğe hakkında bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-126">At each level of the tree, the main pane shows pertinent information about the item.</span></span> <span data-ttu-id="e1e7e-127">Örneğin, belirli bir hizmet için sürüm ve sistem durumunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-127">For example, you can see the health status and version for a particular service.</span></span>

![Service Fabric Explorer essentials bölmesi][sfx-service-essentials]

### <a name="view-the-clusters-nodes"></a><span data-ttu-id="e1e7e-129">Küme düğümlerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e1e7e-129">View the cluster's nodes</span></span>
<span data-ttu-id="e1e7e-130">Düğüm görünümü, kümenin fiziksel düzenini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-130">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="e1e7e-131">Belirli bir düğümde, hangi uygulamalara kod dağıtıldığını denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="e1e7e-132">Daha açık belirtmek gerekirse, çoğaltmalar var. çalışmakta görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="e1e7e-133">Eylemler</span><span class="sxs-lookup"><span data-stu-id="e1e7e-133">Actions</span></span>
<span data-ttu-id="e1e7e-134">Service Fabric Explorer düğümleri, uygulamaları ve Hizmetleri, küme içindeki eylemleri çağırmak için hızlı bir yol sunar.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-134">Service Fabric Explorer offers a quick way to invoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="e1e7e-135">Örneğin, bir uygulama örneği silmek için soldaki ağaç uygulamayı seçin ve ardından **Eylemler** > **uygulama Sil**.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-135">For example, to delete an application instance, choose the application from the tree on the left, and then choose **Actions** > **Delete Application**.</span></span>

![Bir Service Fabric Explorer'da uygulama silme][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="e1e7e-137">Her öğe yanındaki üç nokta işaretine tıklayarak aynı eylemleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-137">You can perform the same actions by clicking the ellipsis next to each element.</span></span>
>
>

<span data-ttu-id="e1e7e-138">Aşağıdaki tabloda her bir varlık için kullanılabilir eylemleri listeler:</span><span class="sxs-lookup"><span data-stu-id="e1e7e-138">The following table lists the actions available for each entity:</span></span>

| <span data-ttu-id="e1e7e-139">**Varlık**</span><span class="sxs-lookup"><span data-stu-id="e1e7e-139">**Entity**</span></span> | <span data-ttu-id="e1e7e-140">**Eylem**</span><span class="sxs-lookup"><span data-stu-id="e1e7e-140">**Action**</span></span> | <span data-ttu-id="e1e7e-141">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="e1e7e-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1e7e-142">Uygulama türü</span><span class="sxs-lookup"><span data-stu-id="e1e7e-142">Application type</span></span> |<span data-ttu-id="e1e7e-143">Sağlamayı kaldırma türü</span><span class="sxs-lookup"><span data-stu-id="e1e7e-143">Unprovision type</span></span> |<span data-ttu-id="e1e7e-144">Uygulama paketi kümenin görüntü deposundan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-144">Removes the application package from the cluster's image store.</span></span> <span data-ttu-id="e1e7e-145">Bu türdeki tüm uygulamaları önce kaldırılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-145">Requires all applications of that type to be removed first.</span></span> |
| <span data-ttu-id="e1e7e-146">Uygulama</span><span class="sxs-lookup"><span data-stu-id="e1e7e-146">Application</span></span> |<span data-ttu-id="e1e7e-147">Uygulamayı Silme</span><span class="sxs-lookup"><span data-stu-id="e1e7e-147">Delete Application</span></span> |<span data-ttu-id="e1e7e-148">Tüm hizmetler ve durumlarına (varsa) dahil olmak üzere uygulama silin.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-148">Delete the application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="e1e7e-149">Hizmet</span><span class="sxs-lookup"><span data-stu-id="e1e7e-149">Service</span></span> |<span data-ttu-id="e1e7e-150">Hizmet silme</span><span class="sxs-lookup"><span data-stu-id="e1e7e-150">Delete Service</span></span> |<span data-ttu-id="e1e7e-151">Hizmet ve durumuna (varsa) silin.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-151">Delete the service and its state (if any).</span></span> |
| <span data-ttu-id="e1e7e-152">Node</span><span class="sxs-lookup"><span data-stu-id="e1e7e-152">Node</span></span> |<span data-ttu-id="e1e7e-153">Etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e1e7e-153">Activate</span></span> |<span data-ttu-id="e1e7e-154">Düğüm etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-154">Activate the node.</span></span> |
| <span data-ttu-id="e1e7e-155">Node</span><span class="sxs-lookup"><span data-stu-id="e1e7e-155">Node</span></span> | <span data-ttu-id="e1e7e-156">(Ara) devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="e1e7e-156">Deactivate (pause)</span></span> | <span data-ttu-id="e1e7e-157">Geçerli durumunda düğümü duraklatır.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-157">Pause the node in its current state.</span></span> <span data-ttu-id="e1e7e-158">Hizmetleri çalışmaya devam eder, ancak bir kesinti veya veri tutarsızlığı önlemek için gerekli olmadıkça Service Fabric proaktif olarak herhangi bir şey üzerine veya onu devre dışı taşımaz.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-158">Services continue to run but Service Fabric does not proactively move anything onto or off it unless it is required to prevent an outage or data inconsistency.</span></span> <span data-ttu-id="e1e7e-159">Bu eylem, genellikle belirli bir düğümde İnceleme sırasında taşımayın emin olmak için hata ayıklama hizmetlerini etkinleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-159">This action is typically used to enable debugging services on a specific node to ensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="e1e7e-160">Node</span><span class="sxs-lookup"><span data-stu-id="e1e7e-160">Node</span></span> | <span data-ttu-id="e1e7e-161">(Yeniden) devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="e1e7e-161">Deactivate (restart)</span></span> | <span data-ttu-id="e1e7e-162">Güvenli bir şekilde tüm bellek içi Hizmetleri bir düğümü kapalı ve kalıcı Hizmetleri kapatın taşıyın.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="e1e7e-163">Genellikle kullanılmaz ana bilgisayar işlemlerini ya da makinenin yeniden başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-163">Typically used when the host processes or machine need to be restarted.</span></span> | |
| <span data-ttu-id="e1e7e-164">Node</span><span class="sxs-lookup"><span data-stu-id="e1e7e-164">Node</span></span> | <span data-ttu-id="e1e7e-165">(Verileri Kaldır) devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="e1e7e-165">Deactivate (remove data)</span></span> | <span data-ttu-id="e1e7e-166">Güvenli bir şekilde yeterli yedek çoğaltmaları oluşturduktan sonra düğüm üzerinde çalışan tüm hizmetleri kapatın.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-166">Safely close all services running on the node after building sufficient spare replicas.</span></span> <span data-ttu-id="e1e7e-167">Genellikle bir düğümü kullanılır (veya en az depolama alanı) dışında Komisyonu kalıcı olarak kullanıldığını.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="e1e7e-168">Node</span><span class="sxs-lookup"><span data-stu-id="e1e7e-168">Node</span></span> | <span data-ttu-id="e1e7e-169">Düğüm durumu Kaldır</span><span class="sxs-lookup"><span data-stu-id="e1e7e-169">Remove node state</span></span> | <span data-ttu-id="e1e7e-170">Bir düğümün çoğaltmaları bilgisi kümeden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-170">Remove knowledge of a node's replicas from the cluster.</span></span> <span data-ttu-id="e1e7e-171">Genellikle, zaten başarısız olan bir düğümün kurtarılamaz kabul edilir olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="e1e7e-172">Node</span><span class="sxs-lookup"><span data-stu-id="e1e7e-172">Node</span></span> | <span data-ttu-id="e1e7e-173">Yeniden Başlatma</span><span class="sxs-lookup"><span data-stu-id="e1e7e-173">Restart</span></span> | <span data-ttu-id="e1e7e-174">Bir düğüm düğümü yeniden başlatarak arızanın benzetimini gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-174">Simulate a node failure by restarting the node.</span></span> <span data-ttu-id="e1e7e-175">Daha fazla bilgi [burada](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="e1e7e-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="e1e7e-176">Birçok Eylemler bozucu olduğundan, işlem tamamlanmadan önce maksadınızı onaylamak için istenebilir.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-176">Since many actions are destructive, you may be asked to confirm your intent before the action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="e1e7e-177">Service Fabric Explorer gerçekleştirilebilir her eylem otomasyonunu sağlamak için PowerShell veya bir REST API'si gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, to enable automation.</span></span>
>
>

<span data-ttu-id="e1e7e-178">Service Fabric Explorer, verilen uygulama türü ve sürümü için uygulama örnekleri oluşturmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-178">You can also use Service Fabric Explorer to create application instances for a given application type and version.</span></span> <span data-ttu-id="e1e7e-179">Ağaç görünümünde uygulama türünü seçin ve ardından **oluşturma uygulama örneği** gibi sağ bölmede sürüm yanındaki bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-179">Choose the application type in the tree view, then click the **Create app instance** link next to the version you'd like in the right pane.</span></span>

![Service Fabric Explorer'da uygulama örneğini oluşturma][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="e1e7e-181">Service Fabric Explorer ile oluşturulan uygulama örnekleri şu anda parametreli olamaz.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="e1e7e-182">Bunlar, varsayılan parametre değerleri kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-to-a-remote-service-fabric-cluster"></a><span data-ttu-id="e1e7e-183">Uzak bir Service Fabric kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="e1e7e-183">Connect to a remote Service Fabric cluster</span></span>
<span data-ttu-id="e1e7e-184">Kümenin endpoint biliyor ve yeterli izinlere sahip herhangi bir tarayıcıdan Service Fabric Explorer erişebilir.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-184">If you know the cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="e1e7e-185">Service Fabric Explorer kümede çalışan başka bir hizmete olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-185">This is because Service Fabric Explorer is just another service that runs in the cluster.</span></span>

### <a name="discover-the-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="e1e7e-186">Uzak bir küme için Service Fabric Explorer uç noktası bulunamadı</span><span class="sxs-lookup"><span data-stu-id="e1e7e-186">Discover the Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="e1e7e-187">Belirli bir küme için Service Fabric Explorer ulaşmak için tarayıcınızı noktası:</span><span class="sxs-lookup"><span data-stu-id="e1e7e-187">To reach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="e1e7e-188">http://&lt;küme endpoint bilgisayarınızı&gt;: 19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="e1e7e-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="e1e7e-189">Azure kümeleri için tam URL de Azure Portalı'nın küme essentials bölmesinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-189">For Azure clusters, the full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="e1e7e-190">Güvenli bir kümeye bağlanma</span><span class="sxs-lookup"><span data-stu-id="e1e7e-190">Connect to a secure cluster</span></span>
<span data-ttu-id="e1e7e-191">Service Fabric kümenize, sertifikalar veya Azure Active Directory (AAD) kullanarak, istemci erişimi denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-191">You can control client access to your Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="e1e7e-192">Service Fabric Gezgini'ne güvenli bir kümede bağlanmaya çalışırsanız, ardından kümenin yapılandırmasına bağlı olarak, bir istemci sertifikası sunan veya AAD kullanarak oturum gerekecek.</span><span class="sxs-lookup"><span data-stu-id="e1e7e-192">If you attempt to connect to Service Fabric Explorer on a secure cluster, then depending on the cluster's configuration you'll be required to present a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1e7e-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1e7e-193">Next steps</span></span>
* [<span data-ttu-id="e1e7e-194">Test Edilebilirlik genel bakış</span><span class="sxs-lookup"><span data-stu-id="e1e7e-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="e1e7e-195">Visual Studio'da, Service Fabric uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="e1e7e-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="e1e7e-196">PowerShell kullanarak Service Fabric uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="e1e7e-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
