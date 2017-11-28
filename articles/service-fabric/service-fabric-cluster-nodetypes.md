---
title: "Service Fabric düğüm türleri ve VM ölçek kümesi | Microsoft Docs"
description: "Service Fabric düğüm türleri VM ölçek kümesi ile ilgili ve nasıl uzak bir VM ölçek kümesi örneği veya bir küme düğümüne bağlanmak nasıl açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 3b1a22bb3653abb68fc73645ad2cb623fabc7736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="the-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="45ee2-103">Service Fabric düğüm türleri ve sanal makine ölçek kümeleri arasındaki ilişki</span><span class="sxs-lookup"><span data-stu-id="45ee2-103">The relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="45ee2-104">Sanal makine ölçek kümeleri dağıtmak ve sanal makinelerin bir koleksiyon kümesi olarak yönetmek için kullanabileceğiniz bir Azure işlem kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="45ee2-104">Virtual Machine Scale Sets are an Azure Compute resource you can use to deploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="45ee2-105">Service Fabric kümesi içinde tanımlanan her düğüm türü bir ayrı VM ölçek kümesi ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="45ee2-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="45ee2-106">Her düğüm türü sonra ölçeklendirilebilir veya Aşağı bağımsız olarak, farklı bağlantı noktalarının açık olması ve farklı kapasite ölçümlerini olabilir.</span><span class="sxs-lookup"><span data-stu-id="45ee2-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="45ee2-107">Aşağıdaki ekran görüntüsünde iki düğüm türü olan bir küme gösterir: ön uç ve arka uç.</span><span class="sxs-lookup"><span data-stu-id="45ee2-107">The following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="45ee2-108">Her düğüm türü her beş düğüm yok.</span><span class="sxs-lookup"><span data-stu-id="45ee2-108">Each node type has five nodes each.</span></span>

![İki düğüm türleri olan kümesinin ekran görüntüsü][NodeTypes]

## <a name="mapping-vm-scale-set-instances-to-nodes"></a><span data-ttu-id="45ee2-110">VM ölçek kümesi örneklerinin düğümlerine eşleme</span><span class="sxs-lookup"><span data-stu-id="45ee2-110">Mapping VM Scale Set instances to nodes</span></span>
<span data-ttu-id="45ee2-111">Yukarıda gördüğünüz gibi VM ölçek kümesi örneklerinin örneğinden 0'ı ve ardından gelecek oluşturan başlatın.</span><span class="sxs-lookup"><span data-stu-id="45ee2-111">As you can see above, the VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="45ee2-112">Numaralandırma adlarında yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="45ee2-112">The numbering is reflected in the names.</span></span> <span data-ttu-id="45ee2-113">Örneğin, BackEnd_0 0 arka uç VM ölçek kümesi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="45ee2-113">For example, BackEnd_0 is instance 0 of the BackEnd VM Scale Set.</span></span> <span data-ttu-id="45ee2-114">Belirli bu VM ölçek kümesi BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 ve BackEnd_4 adlı beş örneğine sahip.</span><span class="sxs-lookup"><span data-stu-id="45ee2-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="45ee2-115">Bir VM ölçek kümesi ölçeklendirdiğinizde yeni bir örneği oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="45ee2-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="45ee2-116">Yeni VM ölçek kümesi örnek adı genellikle olacaktır VM ölçek kümesi adı + sonraki örneği sayısı.</span><span class="sxs-lookup"><span data-stu-id="45ee2-116">The new VM Scale Set instance name will typically be the VM Scale Set name + the next instance number.</span></span> <span data-ttu-id="45ee2-117">Bizim örneğimizde, BackEnd_5 değil.</span><span class="sxs-lookup"><span data-stu-id="45ee2-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-to-each-node-typevm-scale-set"></a><span data-ttu-id="45ee2-118">VM ölçek eşleme yük dengeleyici her düğüm türü/VM ölçek kümesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="45ee2-118">Mapping VM scale set load balancers to each node type/VM Scale Set</span></span>
<span data-ttu-id="45ee2-119">Sonra kümenizi portalından dağıtmış olan ya da bir kaynak grubundaki tüm kaynakların bir listesini aldığınızda sağlamış olduğumuz, ardından örnek Resource Manager şablonu kullanmış her VM ölçek kümesi veya düğüm türü için yük Dengeleyiciler görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="45ee2-119">If you have deployed your cluster from the portal or have used the sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see the load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="45ee2-120">Adı şöyle olur: **LB -&lt;NodeType adı&gt;**.</span><span class="sxs-lookup"><span data-stu-id="45ee2-120">The name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="45ee2-121">Örneğin, LB-sfcluster4doc-bu ekran görüntüsünde gösterildiği gibi 0:</span><span class="sxs-lookup"><span data-stu-id="45ee2-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Kaynaklar][Resources]

## <a name="remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="45ee2-123">Uzaktan bağlantı VM ölçek kümesi örneği veya bir küme düğümü</span><span class="sxs-lookup"><span data-stu-id="45ee2-123">Remote connect to a VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="45ee2-124">Bir kümede tanımlanan her düğüm türü bir ayrı VM ölçek kümesi ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="45ee2-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="45ee2-125">Düğüm türleri ölçeklendirilmiş anlamına yukarı veya Aşağı bağımsız olarak ve farklı VM SKU'ları yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="45ee2-125">That means the node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="45ee2-126">Sanal makineleri tek örnek VM ölçek kümesi örnekleri kendi sanal bir IP adresi al değil.</span><span class="sxs-lookup"><span data-stu-id="45ee2-126">Unlike single instance VMs, the VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="45ee2-127">Bu nedenle, bir IP adresi için aradığınız ve kullanabileceğiniz uzak bağlantı noktası belirli bir örneğine bağlanmak biraz zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="45ee2-127">So it can be a bit challenging when you are looking for an IP address and port that you can use to remote connect to a specific instance.</span></span>

<span data-ttu-id="45ee2-128">Bunları bulmak için izleyebileceğiniz adımlar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="45ee2-128">Here are the steps you can follow to discover them.</span></span>

### <a name="step-1-find-out-the-virtual-ip-address-for-the-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="45ee2-129">1. adım: düğüm türü için sanal IP adresi ve gelen NAT kuralları RDP öğrenin</span><span class="sxs-lookup"><span data-stu-id="45ee2-129">Step 1: Find out the virtual IP address for the node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="45ee2-130">Alabilmek için kaynak tanımı için bir parçası olarak tanımlanan gelen NAT kuralları değerleri almanız gereken **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="45ee2-130">In order to get that, you need to get the inbound NAT rules values that were defined as a part of the resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="45ee2-131">Portalda, yük dengeleyici dikey penceresine gidin ve ardından **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="45ee2-131">In the portal, navigate to the Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="45ee2-133">İçinde **ayarları**, tıklayın **gelen NAT kuralları**.</span><span class="sxs-lookup"><span data-stu-id="45ee2-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="45ee2-134">Bu artık IP adresini verir ve kullanabileceğiniz uzak bağlantı noktası ilk VM ölçek kümesi örneğine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="45ee2-134">This now gives you the IP address and port that you can use to remote connect to the first VM Scale Set instance.</span></span> <span data-ttu-id="45ee2-135">Aşağıdaki ekran görüntüsünde, olmasından **104.42.106.156** ve **3389**</span><span class="sxs-lookup"><span data-stu-id="45ee2-135">In the screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-the-port-that-you-can-use-to-remote-connect-to-the-specific-vm-scale-set-instancenode"></a><span data-ttu-id="45ee2-137">2. adım: uzaktan için kullandığınız bağlantı noktası belirli VM ölçek kümesi örnek/düğüme bağlanmak çıkış Bul</span><span class="sxs-lookup"><span data-stu-id="45ee2-137">Step 2: Find out the port that you can use to remote connect to the specific VM Scale Set instance/node</span></span>
<span data-ttu-id="45ee2-138">Bu belgede daha önce VM ölçek kümesi örneklerinin düğümlerine nasıl eşleneceğine hakkında açıklandı.</span><span class="sxs-lookup"><span data-stu-id="45ee2-138">Earlier in this document, I talked about how the VM Scale Set instances map to the nodes.</span></span> <span data-ttu-id="45ee2-139">Tam bağlantı noktasına bulmak için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="45ee2-139">We will use that to figure out the exact port.</span></span>

<span data-ttu-id="45ee2-140">Bağlantı noktaları, VM ölçek kümesi örnek artan düzende ayrılır.</span><span class="sxs-lookup"><span data-stu-id="45ee2-140">The ports are allocated in ascending order of the VM Scale Set instance.</span></span> <span data-ttu-id="45ee2-141">Bu nedenle ön uç düğüm türü için my örnekte beş örneklerinin her biri için bağlantı noktalarını aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="45ee2-141">so in my example for the FrontEnd node type, the ports for each of the five instances are the following.</span></span> <span data-ttu-id="45ee2-142">Şimdi VM ölçek kümesi Örneğiniz için aynı eşleme yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="45ee2-142">you now need to do the same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="45ee2-143">**VM ölçek kümesi örneği**</span><span class="sxs-lookup"><span data-stu-id="45ee2-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="45ee2-144">**Bağlantı Noktası**</span><span class="sxs-lookup"><span data-stu-id="45ee2-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="45ee2-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="45ee2-145">FrontEnd_0</span></span> |<span data-ttu-id="45ee2-146">3389</span><span class="sxs-lookup"><span data-stu-id="45ee2-146">3389</span></span> |
| <span data-ttu-id="45ee2-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="45ee2-147">FrontEnd_1</span></span> |<span data-ttu-id="45ee2-148">3390</span><span class="sxs-lookup"><span data-stu-id="45ee2-148">3390</span></span> |
| <span data-ttu-id="45ee2-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="45ee2-149">FrontEnd_2</span></span> |<span data-ttu-id="45ee2-150">3391</span><span class="sxs-lookup"><span data-stu-id="45ee2-150">3391</span></span> |
| <span data-ttu-id="45ee2-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="45ee2-151">FrontEnd_3</span></span> |<span data-ttu-id="45ee2-152">3392</span><span class="sxs-lookup"><span data-stu-id="45ee2-152">3392</span></span> |
| <span data-ttu-id="45ee2-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="45ee2-153">FrontEnd_4</span></span> |<span data-ttu-id="45ee2-154">3393</span><span class="sxs-lookup"><span data-stu-id="45ee2-154">3393</span></span> |
| <span data-ttu-id="45ee2-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="45ee2-155">FrontEnd_5</span></span> |<span data-ttu-id="45ee2-156">3394</span><span class="sxs-lookup"><span data-stu-id="45ee2-156">3394</span></span> |

### <a name="step-3-remote-connect-to-the-specific-vm-scale-set-instance"></a><span data-ttu-id="45ee2-157">3. adım: Uzaktan bağlanmak için belirli VM ölçek kümesi örneği</span><span class="sxs-lookup"><span data-stu-id="45ee2-157">Step 3: Remote connect to the specific VM Scale Set instance</span></span>
<span data-ttu-id="45ee2-158">Aşağıdaki ekran görüntüsünde, t FrontEnd_1 bağlanmak için Uzak Masaüstü bağlantısı kullanın:</span><span class="sxs-lookup"><span data-stu-id="45ee2-158">In the screenshot below I use Remote Desktop Connection to connect to the FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-to-change-the-rdp-port-range-values"></a><span data-ttu-id="45ee2-160">RDP bağlantı noktası aralığı değerlerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="45ee2-160">How to change the RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="45ee2-161">Küme dağıtım öncesinde</span><span class="sxs-lookup"><span data-stu-id="45ee2-161">Before cluster deployment</span></span>
<span data-ttu-id="45ee2-162">Bir Resource Manager şablonu kullanarak kümeyi ayarlarken aralığında belirtebilirsiniz **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="45ee2-162">When you are setting up the cluster using an Resource Manager template, you can specify the range in the **inboundNatPools**.</span></span>

<span data-ttu-id="45ee2-163">İçin kaynak tanımı gidin **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="45ee2-163">Go to the resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="45ee2-164">Altında Bul açıklaması **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="45ee2-164">Under that you find the description for **inboundNatPools**.</span></span>  <span data-ttu-id="45ee2-165">Değiştir *frontendPortRangeStart* ve *frontendportrangeend değeri* değerleri.</span><span class="sxs-lookup"><span data-stu-id="45ee2-165">Replace the *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![InboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="45ee2-167">Küme dağıtım sonrası</span><span class="sxs-lookup"><span data-stu-id="45ee2-167">After cluster deployment</span></span>
<span data-ttu-id="45ee2-168">Bu biraz daha karmaşıktır ve silinmesini VM'ler neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="45ee2-168">This is a bit more involved and may result in the VMs getting recycled.</span></span> <span data-ttu-id="45ee2-169">Artık Azure PowerShell'i kullanarak yeni değerleri ayarlamak bulunacaktır.</span><span class="sxs-lookup"><span data-stu-id="45ee2-169">You will now have to set new values using Azure PowerShell.</span></span> <span data-ttu-id="45ee2-170">Azure PowerShell 1.0 veya üstü makinenize yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="45ee2-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="45ee2-171">Daha önceden yapmadıysanız ı kesinlikle özetlenen adımları izleyin önermek [nasıl Azure PowerShell'i yükleme ve yapılandırma.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="45ee2-171">If you have not done this before, I strongly suggest that you follow the steps outlined in [How to install and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="45ee2-172">Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="45ee2-172">Sign in to your Azure account.</span></span> <span data-ttu-id="45ee2-173">Bu PowerShell komutunu herhangi bir nedenden dolayı başarısız olursa, doğru şekilde yüklenmemiş Azure PowerShell yüklü olup olmadığını kontrol etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="45ee2-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="45ee2-174">Yük dengeleyicide ayrıntıları almak için aşağıdaki komutu çalıştırın ve değerlerin açıklaması için bkz: **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="45ee2-174">Run the following to get details on your load balancer and you see the values for the description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="45ee2-175">Şimdi *frontendportrangeend değeri* ve *frontendPortRangeStart* istediğiniz değerleri.</span><span class="sxs-lookup"><span data-stu-id="45ee2-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* to the values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use the API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="45ee2-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="45ee2-176">Next steps</span></span>
* [<span data-ttu-id="45ee2-177">"Her yere dağıtma" özelliği ve Azure tarafından yönetilen kümeleriyle karşılaştırma genel bakış</span><span class="sxs-lookup"><span data-stu-id="45ee2-177">Overview of the "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="45ee2-178">Küme güvenliği</span><span class="sxs-lookup"><span data-stu-id="45ee2-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="45ee2-179">Service Fabric SDK ve çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="45ee2-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
