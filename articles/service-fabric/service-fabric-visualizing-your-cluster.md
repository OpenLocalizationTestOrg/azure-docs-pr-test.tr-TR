---
title: "aaaVisualizing Service Fabric Explorer kullanarak kümenizi | Microsoft Docs"
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
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="69fef-103">Service Fabric Explorer ile kümenizi görselleştirme</span><span class="sxs-lookup"><span data-stu-id="69fef-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="69fef-104">Service Fabric Explorer inceleme ve uygulamaları ve bir Azure Service Fabric kümesindeki düğümler yönetmek için bir web tabanlı araçtır.</span><span class="sxs-lookup"><span data-stu-id="69fef-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="69fef-105">Her zaman kümenizi nerede çalıştığına bakmaksızın kullanılabilir olması için Service Fabric Explorer doğrudan hello küme içinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="69fef-105">Service Fabric Explorer is hosted directly within hello cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="69fef-106">Video öğretici</span><span class="sxs-lookup"><span data-stu-id="69fef-106">Video tutorial</span></span>

<span data-ttu-id="69fef-107">nasıl toouse Service Fabric Explorer izleme toolearn Microsoft Virtual Academy video aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="69fef-107">toolearn how toouse Service Fabric Explorer, watch hello following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a><span data-ttu-id="69fef-108">TooService Fabric Explorer Bağlan</span><span class="sxs-lookup"><span data-stu-id="69fef-108">Connect tooService Fabric Explorer</span></span>
<span data-ttu-id="69fef-109">Çok hello yönergeleri izlediyseniz[geliştirme ortamınızı hazırlama](service-fabric-get-started.md), toohttp://localhost:19080 giderek yerel kümenizde Service Fabric Explorer başlatabilirsiniz / Explorer.</span><span class="sxs-lookup"><span data-stu-id="69fef-109">If you have followed hello instructions too[prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating toohttp://localhost:19080/Explorer.</span></span>

## <a name="understand-hello-service-fabric-explorer-layout"></a><span data-ttu-id="69fef-110">Merhaba Service Fabric Explorer düzeni anlama</span><span class="sxs-lookup"><span data-stu-id="69fef-110">Understand hello Service Fabric Explorer layout</span></span>
<span data-ttu-id="69fef-111">Service Fabric Explorer ile Merhaba solda hello ağacını kullanarak gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69fef-111">You can navigate through Service Fabric Explorer by using hello tree on hello left.</span></span> <span data-ttu-id="69fef-112">Merhaba ağaç Hello kökünde, hello küme Panosu uygulama ve düğüm durumu özetini dahil olmak üzere kümenizi genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="69fef-112">At hello root of hello tree, hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Service Fabric Explorer küme Panosu][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a><span data-ttu-id="69fef-114">Merhaba kümenin düzeni görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="69fef-114">View hello cluster's layout</span></span>
<span data-ttu-id="69fef-115">Bir Service Fabric kümesindeki düğümler hata etki alanı arasında iki boyutlu bir kılavuz yerleştirilir ve etki alanlarını yükseltme.</span><span class="sxs-lookup"><span data-stu-id="69fef-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="69fef-116">Bu yerleştirme uygulamalarınızı ve donanım hatalarına uygulama yükseltmeleri hello bulunması kullanılabilir kalmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="69fef-116">This placement ensures that your applications remain available in hello presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="69fef-117">Nasıl hello geçerli küme hello küme eşlemesi kullanarak düzenlendiğini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69fef-117">You can view how hello current cluster is laid out by using hello cluster map.</span></span>

![Service Fabric Explorer küme eşleme][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="69fef-119">Görünüm uygulamaları ve Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="69fef-119">View applications and services</span></span>
<span data-ttu-id="69fef-120">Merhaba küme iki alt ağaçları içerir: biri uygulamaları ve diğer düğümleri için.</span><span class="sxs-lookup"><span data-stu-id="69fef-120">hello cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="69fef-121">Service Fabric'ın mantıksal hiyerarşisi aracılığıyla hello uygulama görünümü toonavigate kullanabilirsiniz: uygulamaları, hizmetleri, bölümler ve çoğaltmalar.</span><span class="sxs-lookup"><span data-stu-id="69fef-121">You can use hello application view toonavigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="69fef-122">Merhaba aşağıdaki örnekte, uygulama hello **Uygulamam** iki hizmetinden, oluşan **Mystatefulservice'ten** ve **WebService**.</span><span class="sxs-lookup"><span data-stu-id="69fef-122">In hello example below, hello application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="69fef-123">Bu yana **Mystatefulservice'ten** durum bilgisi olan bir birincil ve iki ikincil çoğaltma sahip bir bölüm içerir.</span><span class="sxs-lookup"><span data-stu-id="69fef-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="69fef-124">Bunun aksine, WebSvcService durum bilgisiz ve tek bir örnek içerir.</span><span class="sxs-lookup"><span data-stu-id="69fef-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Service Fabric Explorer uygulama görünümü][sfx-application-tree]

<span data-ttu-id="69fef-126">Her hello ağacı düzeyinde hello ana bölmede hello öğe hakkında bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="69fef-126">At each level of hello tree, hello main pane shows pertinent information about hello item.</span></span> <span data-ttu-id="69fef-127">Örneğin, hello sistem durumunu ve belirli bir hizmet için sürüm görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69fef-127">For example, you can see hello health status and version for a particular service.</span></span>

![Service Fabric Explorer essentials bölmesi][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a><span data-ttu-id="69fef-129">Merhaba kümenin düğümlerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="69fef-129">View hello cluster's nodes</span></span>
<span data-ttu-id="69fef-130">Merhaba düğümü görünüm hello küme hello fiziksel düzenini gösterir.</span><span class="sxs-lookup"><span data-stu-id="69fef-130">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="69fef-131">Belirli bir düğümde, hangi uygulamalara kod dağıtıldığını denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69fef-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="69fef-132">Daha açık belirtmek gerekirse, çoğaltmalar var. çalışmakta görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69fef-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="69fef-133">Eylemler</span><span class="sxs-lookup"><span data-stu-id="69fef-133">Actions</span></span>
<span data-ttu-id="69fef-134">Service Fabric Explorer Eylemler düğümleri, uygulamaları ve Hizmetleri, küme içindeki bir hızlı yol tooinvoke sunar.</span><span class="sxs-lookup"><span data-stu-id="69fef-134">Service Fabric Explorer offers a quick way tooinvoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="69fef-135">Örneğin, toodelete uygulama örneğini hello soldaki hello ağacından hello uygulamayı seçin ve ardından **Eylemler** > **uygulama Sil**.</span><span class="sxs-lookup"><span data-stu-id="69fef-135">For example, toodelete an application instance, choose hello application from hello tree on hello left, and then choose **Actions** > **Delete Application**.</span></span>

![Bir Service Fabric Explorer'da uygulama silme][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="69fef-137">Gerçekleştirebileceğiniz hello aynı eylemleri hello üç nokta sonraki tooeach öğeye tıklayarak.</span><span class="sxs-lookup"><span data-stu-id="69fef-137">You can perform hello same actions by clicking hello ellipsis next tooeach element.</span></span>
>
>

<span data-ttu-id="69fef-138">Merhaba aşağıdaki tabloda her bir varlık için kullanılabilir hello eylemleri listeler:</span><span class="sxs-lookup"><span data-stu-id="69fef-138">hello following table lists hello actions available for each entity:</span></span>

| <span data-ttu-id="69fef-139">**Varlık**</span><span class="sxs-lookup"><span data-stu-id="69fef-139">**Entity**</span></span> | <span data-ttu-id="69fef-140">**Eylem**</span><span class="sxs-lookup"><span data-stu-id="69fef-140">**Action**</span></span> | <span data-ttu-id="69fef-141">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="69fef-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69fef-142">Uygulama türü</span><span class="sxs-lookup"><span data-stu-id="69fef-142">Application type</span></span> |<span data-ttu-id="69fef-143">Sağlamayı kaldırma türü</span><span class="sxs-lookup"><span data-stu-id="69fef-143">Unprovision type</span></span> |<span data-ttu-id="69fef-144">Merhaba uygulama paketi hello kümenin görüntü deposundan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="69fef-144">Removes hello application package from hello cluster's image store.</span></span> <span data-ttu-id="69fef-145">Bu tür toobe önce kaldırılan tüm uygulamaları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="69fef-145">Requires all applications of that type toobe removed first.</span></span> |
| <span data-ttu-id="69fef-146">Uygulama</span><span class="sxs-lookup"><span data-stu-id="69fef-146">Application</span></span> |<span data-ttu-id="69fef-147">Uygulamayı Silme</span><span class="sxs-lookup"><span data-stu-id="69fef-147">Delete Application</span></span> |<span data-ttu-id="69fef-148">Merhaba uygulaması, tüm hizmetler ve durumlarına (varsa) dahil olmak üzere silin.</span><span class="sxs-lookup"><span data-stu-id="69fef-148">Delete hello application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="69fef-149">Hizmet</span><span class="sxs-lookup"><span data-stu-id="69fef-149">Service</span></span> |<span data-ttu-id="69fef-150">Hizmet silme</span><span class="sxs-lookup"><span data-stu-id="69fef-150">Delete Service</span></span> |<span data-ttu-id="69fef-151">Merhaba hizmeti ve durumuna (varsa) silin.</span><span class="sxs-lookup"><span data-stu-id="69fef-151">Delete hello service and its state (if any).</span></span> |
| <span data-ttu-id="69fef-152">Node</span><span class="sxs-lookup"><span data-stu-id="69fef-152">Node</span></span> |<span data-ttu-id="69fef-153">Etkinleştir</span><span class="sxs-lookup"><span data-stu-id="69fef-153">Activate</span></span> |<span data-ttu-id="69fef-154">Merhaba düğümü etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="69fef-154">Activate hello node.</span></span> |
| <span data-ttu-id="69fef-155">Node</span><span class="sxs-lookup"><span data-stu-id="69fef-155">Node</span></span> | <span data-ttu-id="69fef-156">(Ara) devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="69fef-156">Deactivate (pause)</span></span> | <span data-ttu-id="69fef-157">Duraklatma hello düğüm, geçerli durumunda.</span><span class="sxs-lookup"><span data-stu-id="69fef-157">Pause hello node in its current state.</span></span> <span data-ttu-id="69fef-158">Hizmetleri toorun devam ancak gerekli tooprevent kesinti veya veri tutarsızlığına olmadığı sürece Service Fabric proaktif olarak herhangi bir şey üzerine veya onu devre dışı taşımaz.</span><span class="sxs-lookup"><span data-stu-id="69fef-158">Services continue toorun but Service Fabric does not proactively move anything onto or off it unless it is required tooprevent an outage or data inconsistency.</span></span> <span data-ttu-id="69fef-159">İnceleme sırasında taşımayın belirli düğüm tooensure hizmetlerinde hata ayıklama genellikle kullanılan tooenable eylemdir.</span><span class="sxs-lookup"><span data-stu-id="69fef-159">This action is typically used tooenable debugging services on a specific node tooensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="69fef-160">Node</span><span class="sxs-lookup"><span data-stu-id="69fef-160">Node</span></span> | <span data-ttu-id="69fef-161">(Yeniden) devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="69fef-161">Deactivate (restart)</span></span> | <span data-ttu-id="69fef-162">Güvenli bir şekilde tüm bellek içi Hizmetleri bir düğümü kapalı ve kalıcı Hizmetleri kapatın taşıyın.</span><span class="sxs-lookup"><span data-stu-id="69fef-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="69fef-163">Genellikle, Hello ana bilgisayar işlemlerini veya makine gerek toobe başlatıldığında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="69fef-163">Typically used when hello host processes or machine need toobe restarted.</span></span> | |
| <span data-ttu-id="69fef-164">Node</span><span class="sxs-lookup"><span data-stu-id="69fef-164">Node</span></span> | <span data-ttu-id="69fef-165">(Verileri Kaldır) devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="69fef-165">Deactivate (remove data)</span></span> | <span data-ttu-id="69fef-166">Güvenli bir şekilde yeterli yedek çoğaltmaları oluşturduktan sonra hello düğüm üzerinde çalışan tüm hizmetleri kapatın.</span><span class="sxs-lookup"><span data-stu-id="69fef-166">Safely close all services running on hello node after building sufficient spare replicas.</span></span> <span data-ttu-id="69fef-167">Genellikle bir düğümü kullanılır (veya en az depolama alanı) dışında Komisyonu kalıcı olarak kullanıldığını.</span><span class="sxs-lookup"><span data-stu-id="69fef-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="69fef-168">Node</span><span class="sxs-lookup"><span data-stu-id="69fef-168">Node</span></span> | <span data-ttu-id="69fef-169">Düğüm durumu Kaldır</span><span class="sxs-lookup"><span data-stu-id="69fef-169">Remove node state</span></span> | <span data-ttu-id="69fef-170">Bir düğümün çoğaltmaları bilgisi hello kümeden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="69fef-170">Remove knowledge of a node's replicas from hello cluster.</span></span> <span data-ttu-id="69fef-171">Genellikle, zaten başarısız olan bir düğümün kurtarılamaz kabul edilir olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="69fef-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="69fef-172">Node</span><span class="sxs-lookup"><span data-stu-id="69fef-172">Node</span></span> | <span data-ttu-id="69fef-173">Yeniden Başlatma</span><span class="sxs-lookup"><span data-stu-id="69fef-173">Restart</span></span> | <span data-ttu-id="69fef-174">Bir düğüm hello düğümü yeniden başlatarak arızanın benzetimini gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="69fef-174">Simulate a node failure by restarting hello node.</span></span> <span data-ttu-id="69fef-175">Daha fazla bilgi [burada](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="69fef-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="69fef-176">Birçok Eylemler bozucu olduğundan, olabilir hello işlem tamamlanmadan önce tooconfirm maksadınızı istedi.</span><span class="sxs-lookup"><span data-stu-id="69fef-176">Since many actions are destructive, you may be asked tooconfirm your intent before hello action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="69fef-177">Service Fabric Explorer gerçekleştirilebilir her eylem, PowerShell veya tooenable Otomasyon bir REST API'si gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="69fef-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, tooenable automation.</span></span>
>
>

<span data-ttu-id="69fef-178">Service Fabric Explorer toocreate uygulama örnekleri, verilen uygulama türü ve sürümü için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69fef-178">You can also use Service Fabric Explorer toocreate application instances for a given application type and version.</span></span> <span data-ttu-id="69fef-179">Merhaba ağaç görünümünde Hello uygulama türünü seçin ve ardından hello **oluşturma uygulama örneği** gibi hello sağ bölmede bağlantı sonraki toohello sürümü.</span><span class="sxs-lookup"><span data-stu-id="69fef-179">Choose hello application type in hello tree view, then click hello **Create app instance** link next toohello version you'd like in hello right pane.</span></span>

![Service Fabric Explorer'da uygulama örneğini oluşturma][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="69fef-181">Service Fabric Explorer ile oluşturulan uygulama örnekleri şu anda parametreli olamaz.</span><span class="sxs-lookup"><span data-stu-id="69fef-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="69fef-182">Bunlar, varsayılan parametre değerleri kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="69fef-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a><span data-ttu-id="69fef-183">Tooa uzak Service Fabric kümesi Bağlan</span><span class="sxs-lookup"><span data-stu-id="69fef-183">Connect tooa remote Service Fabric cluster</span></span>
<span data-ttu-id="69fef-184">Merhaba kümenin endpoint biliyor ve yeterli izinlere sahip herhangi bir tarayıcıdan Service Fabric Explorer erişebilir.</span><span class="sxs-lookup"><span data-stu-id="69fef-184">If you know hello cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="69fef-185">Service Fabric Explorer hello kümede çalışan başka bir hizmete olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="69fef-185">This is because Service Fabric Explorer is just another service that runs in hello cluster.</span></span>

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="69fef-186">Uzak bir küme için Hello Service Fabric Explorer uç noktası bulunamadı</span><span class="sxs-lookup"><span data-stu-id="69fef-186">Discover hello Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="69fef-187">belirli bir küme için Service Fabric Explorer tooreach tarayıcınıza noktası:</span><span class="sxs-lookup"><span data-stu-id="69fef-187">tooreach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="69fef-188">http://&lt;küme endpoint bilgisayarınızı&gt;: 19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="69fef-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="69fef-189">Azure kümeleri için hello tam URL'yi de hello küme essentials bölmesinde hello Azure portalında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="69fef-189">For Azure clusters, hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="69fef-190">Tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="69fef-190">Connect tooa secure cluster</span></span>
<span data-ttu-id="69fef-191">İstemci erişim tooyour Service Fabric kümesi, sertifikalar veya Azure Active Directory (AAD) kullanarak kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69fef-191">You can control client access tooyour Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="69fef-192">Güvenli bir kümede tooconnect tooService Fabric Explorer çalışırsanız, sonra hello kümenin yapılandırmasına bağlı olarak, gerekli toopresent bir istemci sertifikası veya AAD kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="69fef-192">If you attempt tooconnect tooService Fabric Explorer on a secure cluster, then depending on hello cluster's configuration you'll be required toopresent a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69fef-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="69fef-193">Next steps</span></span>
* [<span data-ttu-id="69fef-194">Test Edilebilirlik genel bakış</span><span class="sxs-lookup"><span data-stu-id="69fef-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="69fef-195">Visual Studio'da, Service Fabric uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="69fef-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="69fef-196">PowerShell kullanarak Service Fabric uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="69fef-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
