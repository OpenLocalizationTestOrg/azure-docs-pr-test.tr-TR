---
title: "aaaService doku düğüm türleri ve VM ölçek kümesi | Microsoft Docs"
description: "Service Fabric düğüm türleri tooVM ölçek kümeleri nasıl ilişkili olduğunu ve tooremote nasıl bağlanacağını tooa VM ölçek kümesi örneği veya bir küme düğümü açıklar."
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
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="b539f-103">Service Fabric düğüm türleri ve sanal makine ölçek kümeleri arasındaki Hello ilişki</span><span class="sxs-lookup"><span data-stu-id="b539f-103">hello relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="b539f-104">Sanal makine ölçek kümeleri toodeploy kullanın ve sanal makinelerin bir koleksiyon kümesi olarak yönetmek bir Azure işlem kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="b539f-104">Virtual Machine Scale Sets are an Azure Compute resource you can use toodeploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="b539f-105">Service Fabric kümesi içinde tanımlanan her düğüm türü bir ayrı VM ölçek kümesi ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b539f-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="b539f-106">Her düğüm türü sonra ölçeklendirilebilir veya Aşağı bağımsız olarak, farklı bağlantı noktalarının açık olması ve farklı kapasite ölçümlerini olabilir.</span><span class="sxs-lookup"><span data-stu-id="b539f-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="b539f-107">Aşağıdaki ekran görüntüsü hello iki düğüm türü olan bir küme gösterir: ön uç ve arka uç.</span><span class="sxs-lookup"><span data-stu-id="b539f-107">hello following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="b539f-108">Her düğüm türü her beş düğüm yok.</span><span class="sxs-lookup"><span data-stu-id="b539f-108">Each node type has five nodes each.</span></span>

![İki düğüm türleri olan kümesinin ekran görüntüsü][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a><span data-ttu-id="b539f-110">VM ölçek kümesi örneklerinin toonodes eşleme</span><span class="sxs-lookup"><span data-stu-id="b539f-110">Mapping VM Scale Set instances toonodes</span></span>
<span data-ttu-id="b539f-111">Yukarıda gördüğünüz gibi hello VM ölçek kümesi örneklerinin 0 örneğinden başlatın ve sonra artar.</span><span class="sxs-lookup"><span data-stu-id="b539f-111">As you can see above, hello VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="b539f-112">Merhaba numaralandırma hello adlarında yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="b539f-112">hello numbering is reflected in hello names.</span></span> <span data-ttu-id="b539f-113">Örneğin, BackEnd_0 0 hello arka uç VM ölçek kümesi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="b539f-113">For example, BackEnd_0 is instance 0 of hello BackEnd VM Scale Set.</span></span> <span data-ttu-id="b539f-114">Belirli bu VM ölçek kümesi BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 ve BackEnd_4 adlı beş örneğine sahip.</span><span class="sxs-lookup"><span data-stu-id="b539f-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="b539f-115">Bir VM ölçek kümesi ölçeklendirdiğinizde yeni bir örneği oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b539f-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="b539f-116">Merhaba yeni VM ölçek kümesi örnek adı genellikle olacaktır hello VM ölçek kümesi adı + hello sonraki örneği sayısı.</span><span class="sxs-lookup"><span data-stu-id="b539f-116">hello new VM Scale Set instance name will typically be hello VM Scale Set name + hello next instance number.</span></span> <span data-ttu-id="b539f-117">Bizim örneğimizde, BackEnd_5 değil.</span><span class="sxs-lookup"><span data-stu-id="b539f-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a><span data-ttu-id="b539f-118">Ölçek kümesini yük Dengeleyiciler tooeach düğüm türü/VM ölçek kümesi VM eşleme</span><span class="sxs-lookup"><span data-stu-id="b539f-118">Mapping VM scale set load balancers tooeach node type/VM Scale Set</span></span>
<span data-ttu-id="b539f-119">Sonra kümenizi hello portalından dağıtmış olan ya da bir kaynak grubundaki tüm kaynakların bir listesini aldığınızda sağlamış olduğumuz, ardından hello örnek Resource Manager şablonu kullanmış her VM ölçek kümesi veya düğüm türü için hello yük Dengeleyiciler görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b539f-119">If you have deployed your cluster from hello portal or have used hello sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see hello load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="b539f-120">Merhaba adı şöyle olur: **LB -&lt;NodeType adı&gt;**.</span><span class="sxs-lookup"><span data-stu-id="b539f-120">hello name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="b539f-121">Örneğin, LB-sfcluster4doc-bu ekran görüntüsünde gösterildiği gibi 0:</span><span class="sxs-lookup"><span data-stu-id="b539f-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Kaynaklar][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="b539f-123">Uzaktan bağlantı tooa VM ölçek kümesi örneği veya bir küme düğümü</span><span class="sxs-lookup"><span data-stu-id="b539f-123">Remote connect tooa VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="b539f-124">Bir kümede tanımlanan her düğüm türü bir ayrı VM ölçek kümesi ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b539f-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="b539f-125">Anlamına gelir düğüm türleri hello Genişletilebilir yukarı veya Aşağı bağımsız olarak ve farklı VM SKU'ları yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="b539f-125">That means hello node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="b539f-126">Sanal makineleri tek örnek hello VM ölçek kümesi örnekleri kendi sanal bir IP adresi al değil.</span><span class="sxs-lookup"><span data-stu-id="b539f-126">Unlike single instance VMs, hello VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="b539f-127">Bir bit olabilir bir IP için bakarken zor adresi ve bağlantı noktası tooremote kullanabileceğiniz tooa belirli örneğe bağlanın.</span><span class="sxs-lookup"><span data-stu-id="b539f-127">So it can be a bit challenging when you are looking for an IP address and port that you can use tooremote connect tooa specific instance.</span></span>

<span data-ttu-id="b539f-128">Toodiscover izleyin hello adımlar şunlardır bunları.</span><span class="sxs-lookup"><span data-stu-id="b539f-128">Here are hello steps you can follow toodiscover them.</span></span>

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="b539f-129">1. adım: hello sanal IP adresi hello düğüm türü için'i ve ardından gelen NAT kuralları RDP öğrenin</span><span class="sxs-lookup"><span data-stu-id="b539f-129">Step 1: Find out hello virtual IP address for hello node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="b539f-130">Tooget hello gerekir, sipariş tooget içinde hello kaynak tanımının bir parçası olarak tanımlanmış olan değerleri gelen NAT kuralları **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="b539f-130">In order tooget that, you need tooget hello inbound NAT rules values that were defined as a part of hello resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="b539f-131">Merhaba Portalı'nda toohello yük dengeleyici dikey gidin ve ardından **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="b539f-131">In hello portal, navigate toohello Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="b539f-133">İçinde **ayarları**, tıklayın **gelen NAT kuralları**.</span><span class="sxs-lookup"><span data-stu-id="b539f-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="b539f-134">Bu şimdi toohello ilk VM ölçek kümesi örnek IP adresi ve bağlantı noktası tooremote kullanabileceğiniz hello verir bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b539f-134">This now gives you hello IP address and port that you can use tooremote connect toohello first VM Scale Set instance.</span></span> <span data-ttu-id="b539f-135">Merhaba ekran görüntüsünde, olmasından **104.42.106.156** ve **3389**</span><span class="sxs-lookup"><span data-stu-id="b539f-135">In hello screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a><span data-ttu-id="b539f-137">2. adım: başlangıç bağlantı noktası tooremote kullanabileceğiniz öğrenin bağlanmak toohello belirli VM ölçek kümesi örnek/düğüm</span><span class="sxs-lookup"><span data-stu-id="b539f-137">Step 2: Find out hello port that you can use tooremote connect toohello specific VM Scale Set instance/node</span></span>
<span data-ttu-id="b539f-138">Bu belgede daha önce hello VM ölçek kümesi örneklerinin toohello düğümleri nasıl eşleneceğine hakkında açıklandı.</span><span class="sxs-lookup"><span data-stu-id="b539f-138">Earlier in this document, I talked about how hello VM Scale Set instances map toohello nodes.</span></span> <span data-ttu-id="b539f-139">Merhaba tam bağlantı noktasına bu toofigure kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="b539f-139">We will use that toofigure out hello exact port.</span></span>

<span data-ttu-id="b539f-140">Merhaba bağlantı noktalarını hello VM ölçek kümesi örnek artan düzende ayrılır.</span><span class="sxs-lookup"><span data-stu-id="b539f-140">hello ports are allocated in ascending order of hello VM Scale Set instance.</span></span> <span data-ttu-id="b539f-141">Bu nedenle hello ön uç düğüm türü için my örnekte, her hello beş örneklerinin hello bağlantı noktalarını hello aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b539f-141">so in my example for hello FrontEnd node type, hello ports for each of hello five instances are hello following.</span></span> <span data-ttu-id="b539f-142">artık toodo VM ölçek kümesi Örneğiniz için aynı eşleme hello.</span><span class="sxs-lookup"><span data-stu-id="b539f-142">you now need toodo hello same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="b539f-143">**VM ölçek kümesi örneği**</span><span class="sxs-lookup"><span data-stu-id="b539f-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="b539f-144">**Bağlantı Noktası**</span><span class="sxs-lookup"><span data-stu-id="b539f-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="b539f-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="b539f-145">FrontEnd_0</span></span> |<span data-ttu-id="b539f-146">3389</span><span class="sxs-lookup"><span data-stu-id="b539f-146">3389</span></span> |
| <span data-ttu-id="b539f-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="b539f-147">FrontEnd_1</span></span> |<span data-ttu-id="b539f-148">3390</span><span class="sxs-lookup"><span data-stu-id="b539f-148">3390</span></span> |
| <span data-ttu-id="b539f-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="b539f-149">FrontEnd_2</span></span> |<span data-ttu-id="b539f-150">3391</span><span class="sxs-lookup"><span data-stu-id="b539f-150">3391</span></span> |
| <span data-ttu-id="b539f-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="b539f-151">FrontEnd_3</span></span> |<span data-ttu-id="b539f-152">3392</span><span class="sxs-lookup"><span data-stu-id="b539f-152">3392</span></span> |
| <span data-ttu-id="b539f-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="b539f-153">FrontEnd_4</span></span> |<span data-ttu-id="b539f-154">3393</span><span class="sxs-lookup"><span data-stu-id="b539f-154">3393</span></span> |
| <span data-ttu-id="b539f-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="b539f-155">FrontEnd_5</span></span> |<span data-ttu-id="b539f-156">3394</span><span class="sxs-lookup"><span data-stu-id="b539f-156">3394</span></span> |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a><span data-ttu-id="b539f-157">3. adım: Uzaktan bağlanma toohello belirli VM ölçek kümesi örneği</span><span class="sxs-lookup"><span data-stu-id="b539f-157">Step 3: Remote connect toohello specific VM Scale Set instance</span></span>
<span data-ttu-id="b539f-158">Uzak Masaüstü Bağlantısı tooconnect toohello FrontEnd_1 kullanmam Hello ekran görüntüsünde:</span><span class="sxs-lookup"><span data-stu-id="b539f-158">In hello screenshot below I use Remote Desktop Connection tooconnect toohello FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a><span data-ttu-id="b539f-160">Nasıl toochange hello RDP bağlantı noktası aralığı değerleri</span><span class="sxs-lookup"><span data-stu-id="b539f-160">How toochange hello RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="b539f-161">Küme dağıtım öncesinde</span><span class="sxs-lookup"><span data-stu-id="b539f-161">Before cluster deployment</span></span>
<span data-ttu-id="b539f-162">Bir Resource Manager şablonu kullanarak hello küme ayarlarken hello hello aralığı belirtebilirsiniz **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="b539f-162">When you are setting up hello cluster using an Resource Manager template, you can specify hello range in hello **inboundNatPools**.</span></span>

<span data-ttu-id="b539f-163">Toohello kaynak tanımı gitmek **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="b539f-163">Go toohello resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="b539f-164">Altında Bul hello açıklamasını **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="b539f-164">Under that you find hello description for **inboundNatPools**.</span></span>  <span data-ttu-id="b539f-165">Hello yerine *frontendPortRangeStart* ve *frontendportrangeend değeri* değerleri.</span><span class="sxs-lookup"><span data-stu-id="b539f-165">Replace hello *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![InboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="b539f-167">Küme dağıtım sonrası</span><span class="sxs-lookup"><span data-stu-id="b539f-167">After cluster deployment</span></span>
<span data-ttu-id="b539f-168">Bu biraz daha karmaşıktır ve silinmesini hello Vm'lerde neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="b539f-168">This is a bit more involved and may result in hello VMs getting recycled.</span></span> <span data-ttu-id="b539f-169">Şimdi, Azure PowerShell kullanarak tooset yeni değerlere sahip olur.</span><span class="sxs-lookup"><span data-stu-id="b539f-169">You will now have tooset new values using Azure PowerShell.</span></span> <span data-ttu-id="b539f-170">Azure PowerShell 1.0 veya üstü makinenize yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b539f-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="b539f-171">Daha önceden yapmadıysanız ı kesinlikle özetlenen hello adımları izleyin önermek [nasıl tooinstall ve Azure PowerShell yapılandırın.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="b539f-171">If you have not done this before, I strongly suggest that you follow hello steps outlined in [How tooinstall and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="b539f-172">İçinde tooyour Azure hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b539f-172">Sign in tooyour Azure account.</span></span> <span data-ttu-id="b539f-173">Bu PowerShell komutunu herhangi bir nedenden dolayı başarısız olursa, doğru şekilde yüklenmemiş Azure PowerShell yüklü olup olmadığını kontrol etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b539f-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="b539f-174">Yük Dengeleyici tooget Ayrıntılar aşağıdaki hello çalıştırın ve hello değerlerini hello açıklamasını görmek **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="b539f-174">Run hello following tooget details on your load balancer and you see hello values for hello description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="b539f-175">Şimdi *frontendportrangeend değeri* ve *frontendPortRangeStart* istediğiniz toohello değerler.</span><span class="sxs-lookup"><span data-stu-id="b539f-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* toohello values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="b539f-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b539f-176">Next steps</span></span>
* [<span data-ttu-id="b539f-177">Merhaba "Herhangi bir yere dağıtma" özelliği ve Azure tarafından yönetilen kümeleriyle karşılaştırma genel bakış</span><span class="sxs-lookup"><span data-stu-id="b539f-177">Overview of hello "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="b539f-178">Küme güvenliği</span><span class="sxs-lookup"><span data-stu-id="b539f-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="b539f-179">Service Fabric SDK ve çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b539f-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
