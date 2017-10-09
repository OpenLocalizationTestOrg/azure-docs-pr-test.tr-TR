---
title: "aaaAzure Service Fabric programlı ölçeklendirme | Microsoft Docs"
description: "Bir Azure Service Fabric kümesi veya ölçeklendirmek programlı olarak toocustom Tetikleyicileri according"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="06af8-103">Service Fabric kümesi programlı olarak ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="06af8-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="06af8-104">Azure Service Fabric kümesi ölçeklendirme temellerini ele alınmıştır belgelerinde üzerinde [küme ölçeklendirme](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="06af8-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="06af8-105">Bu makale nasıl Service Fabric kümeleri üzerinde sanal makine ölçek kümeleri oluşturulur ve el ile veya Otomatik ölçek kurallarla Genişletilebilir kapsar.</span><span class="sxs-lookup"><span data-stu-id="06af8-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="06af8-106">Bu belgede daha Gelişmiş senaryolar için denetleyici Azure ölçeklendirme işlemlerinin programlama yöntemleri bakar.</span><span class="sxs-lookup"><span data-stu-id="06af8-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="06af8-107">Programsal ölçeklendirme nedenleri</span><span class="sxs-lookup"><span data-stu-id="06af8-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="06af8-108">Birçok senaryoda el ile veya Otomatik ölçek kuralı aracılığıyla ölçeklendirme iyi çözümdür.</span><span class="sxs-lookup"><span data-stu-id="06af8-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="06af8-109">Diğer senaryolarda, ancak bunlar sağ sığacak hello olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="06af8-109">In other scenarios, though, they may not be hello right fit.</span></span> <span data-ttu-id="06af8-110">Olası dezavantajları toothese yaklaşımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="06af8-110">Potential drawbacks toothese approaches include:</span></span>

- <span data-ttu-id="06af8-111">El ile ölçeklendirme içinde toolog ve açıkça işlemleri ölçeklendirme isteği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="06af8-111">Manually scaling requires you toolog in and explicitly request scaling operations.</span></span> <span data-ttu-id="06af8-112">Ölçeklendirme işlemlerinin sık veya beklenmeyen zamanlarda gerekirse, bu yaklaşım iyi bir çözüm olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="06af8-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="06af8-113">Otomatik ölçek kuralı sanal makine ölçek kümesindeki bir örneği kaldırdığınızda, Gümüş veya altın dayanıklılık düzeyini hello düğüm türüne sahip olmadığı sürece bunlar otomatik olarak bilgi o düğümün ilişkili hello Service Fabric kümesinden kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="06af8-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from hello associated Service Fabric cluster unless hello node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="06af8-114">Otomatik ölçek kuralı düzeyi Ayarla hello ölçekte (yerine hello Service Fabric düzeyi) çalışması nedeniyle otomatik ölçek kuralı düzgün biçimde kapatılıyor olmadan Service Fabric düğümleri kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06af8-114">Because auto-scale rules work at hello scale set level (rather than at hello Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="06af8-115">Bu utangaç düğüm kaldırma 'hayalet' Service Fabric düğüm durumu ölçek bileşenini işlemlerinden sonra ardınızda.</span><span class="sxs-lookup"><span data-stu-id="06af8-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="06af8-116">Tek bir (veya hizmet) tooperiodically hello Service Fabric kümesindeki kaldırılmış düğüm durumu temizlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="06af8-116">An individual (or a service) would need tooperiodically clean up removed node state in hello Service Fabric cluster.</span></span>
  - <span data-ttu-id="06af8-117">Altın veya gümüş dayanıklılık düzeyine sahip bir düğüm türü otomatik olarak temizler Not düğümleri kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="06af8-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="06af8-118">Vardır, ancak [birçok ölçümleri](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) otomatik ölçek kuralları tarafından desteklenen, hala olduğu sınırlı bir dizi.</span><span class="sxs-lookup"><span data-stu-id="06af8-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="06af8-119">Senaryonuz bu kümesinde kapsanmayan bazı ölçüm göre ölçekleme için çağırırsa, otomatik ölçeklendirme kurallarını iyi bir seçenek olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="06af8-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="06af8-120">Bu sınırlamalar bağlı olarak, daha özelleştirilmiş otomatik ölçekleme modelleri tooimplement isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="06af8-120">Based on these limitations, you may wish tooimplement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="06af8-121">Ölçeklendirme API'leri</span><span class="sxs-lookup"><span data-stu-id="06af8-121">Scaling APIs</span></span>
<span data-ttu-id="06af8-122">Azure API uygulamaları tooprogrammatically iş Service Fabric kümeleri ve sanal makine ölçek kümeleri olanak mevcut.</span><span class="sxs-lookup"><span data-stu-id="06af8-122">Azure APIs exist which allow applications tooprogrammatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="06af8-123">Bu API'leri varolan otomatik ölçeklendirme seçeneği senaryonuz için işe yaramazsa, olası tooimplement özel ölçeklendirme mantık kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="06af8-123">If existing auto-scale options don't work for your scenario, these APIs make it possible tooimplement custom scaling logic.</span></span> 

<span data-ttu-id="06af8-124">Bu 'giriş-yapılan' otomatik ölçeklendirme bir yaklaşım tooimplementing işlevselliği tooadd işlemleri ölçeklendirme bir yeni durum bilgisiz hizmet toohello Service Fabric uygulaması toomanage olduğu.</span><span class="sxs-lookup"><span data-stu-id="06af8-124">One approach tooimplementing this 'home-made' auto-scaling functionality is tooadd a new stateless service toohello Service Fabric application toomanage scaling operations.</span></span> <span data-ttu-id="06af8-125">Merhaba hizmetin içinde `RunAsync` yöntemi, bir dizi Tetikleyicileri belirleyebilir ölçeklendirme (küme boyutu üst sınırı gibi parametreleri denetleniyor ve cooldowns ölçeklendirme dahil) gerekli olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="06af8-125">Within hello service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="06af8-126">Merhaba sanal makine ölçek kümesi etkileşimler için kullanılan API (her iki toocheck hello geçerli sanal makine örnekleri ve sayısını toomodify onu) hello olan [fluent yönetim Azure işlem Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="06af8-126">hello API used for virtual machine scale set interactions (both toocheck hello current number of virtual machine instances and toomodify it) is hello [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="06af8-127">Merhaba fluent işlem kitaplığı, sanal makine ölçek kümeleri ile etkileşmek için kullanımı kolay API sağlar.</span><span class="sxs-lookup"><span data-stu-id="06af8-127">hello fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="06af8-128">Merhaba Service Fabric kümesi kendisi ile toointeract kullanmak [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="06af8-128">toointeract with hello Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="06af8-129">Elbette, kod ölçeklendirme hello toorun bir hizmet olarak gerek yoktur ölçeklendirilmiş hello küme toobe içinde.</span><span class="sxs-lookup"><span data-stu-id="06af8-129">Of course, hello scaling code doesn't need toorun as a service in hello cluster toobe scaled.</span></span> <span data-ttu-id="06af8-130">Her ikisi de `IAzure` ve `FabricClient` hizmeti ölçeklendirme hello kolayca bir konsol uygulaması veya dış hello Service Fabric uygulamadan çalışan Windows hizmeti böylece ilişkili tootheir Azure kaynaklarını uzaktan bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06af8-130">Both `IAzure` and `FabricClient` can connect tootheir associated Azure resources remotely, so hello scaling service could easily be a console application or Windows service running from outside hello Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="06af8-131">Kimlik bilgisi yönetimi</span><span class="sxs-lookup"><span data-stu-id="06af8-131">Credential management</span></span>
<span data-ttu-id="06af8-132">Bir hizmet toohandle ölçekleme yazma bir hello hizmeti mümkün tooaccess sanal makine ölçek kümesi kaynakları etkileşimli oturum açma olmadan olmalıdır iştir.</span><span class="sxs-lookup"><span data-stu-id="06af8-132">One challenge of writing a service toohandle scaling is that hello service must be able tooaccess virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="06af8-133">Merhaba Service Fabric erişme Küme hizmeti ölçeklendirme hello kendi Service Fabric uygulaması değiştirme, ancak kimlik bilgileri gerekli tooaccess kolaydır hello ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="06af8-133">Accessing hello Service Fabric cluster is easy if hello scaling service is modifying its own Service Fabric application, but credentials are needed tooaccess hello scale set.</span></span> <span data-ttu-id="06af8-134">kullanabileceğiniz toolog içinde bir [hizmet sorumlusu](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) hello ile oluşturulan [Azure CLI 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="06af8-134">toolog in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="06af8-135">Bir hizmet sorumlusu aşağıdaki adımları hello ile oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="06af8-135">A service principal can be created with hello following steps:</span></span>

1. <span data-ttu-id="06af8-136">Toohello Azure CLI oturum (`az login`) erişim toohello sanal makine ölçek sahip bir kullanıcı olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="06af8-136">Log in toohello Azure CLI (`az login`) as a user with access toohello virtual machine scale set</span></span>
2. <span data-ttu-id="06af8-137">Merhaba hizmet sorumlusu ile oluşturma`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="06af8-137">Create hello service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="06af8-138">Merhaba AppID ('istemci kimliği' başka bir yerde olarak adlandırılır), adı, şifresi ve Kiracı daha sonra kullanmak için not edin.</span><span class="sxs-lookup"><span data-stu-id="06af8-138">Make note of hello appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="06af8-139">İle görüntülenebilir abonelik Kimliğinizi de gerekir`az account list`</span><span class="sxs-lookup"><span data-stu-id="06af8-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="06af8-140">Merhaba fluent işlem kitaplığı gibi bu kimlik bilgilerini kullanarak oturum açabilir (çekirdek fluent Azure türleri ister Not `IAzure` hello olan [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) paket):</span><span class="sxs-lookup"><span data-stu-id="06af8-140">hello fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

<span data-ttu-id="06af8-141">Aracılığıyla oturum açtıktan sonra ölçek kümesi örnek sayısı sorgulanabilir `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="06af8-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="06af8-142">Ölçeği genişletme</span><span class="sxs-lookup"><span data-stu-id="06af8-142">Scaling out</span></span>
<span data-ttu-id="06af8-143">Merhaba fluent kullanarak Azure işlem SDK, örnekleri yalnızca birkaç aramaları ayarlamak toohello sanal makine ölçek eklenebilir-</span><span class="sxs-lookup"><span data-stu-id="06af8-143">Using hello fluent Azure compute SDK, instances can be added toohello virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="06af8-144">Alternatif olarak, sanal makine ölçek kümesi boyutu PowerShell cmdlet'leri ile yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="06af8-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="06af8-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)Merhaba sanal makine ölçek kümesi nesnesi alabilir.</span><span class="sxs-lookup"><span data-stu-id="06af8-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve hello virtual machine scale set object.</span></span> <span data-ttu-id="06af8-146">Merhaba geçerli kapasite hello depolanacağı `.sku.capacity` özelliği.</span><span class="sxs-lookup"><span data-stu-id="06af8-146">hello current capacity will be stored in hello `.sku.capacity` property.</span></span> <span data-ttu-id="06af8-147">İstenen değer Hello kapasite toohello değiştirme sonra Azure'da ayarlamak hello sanal makine ölçek hello ile güncelleştirilebilir [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) komutu.</span><span class="sxs-lookup"><span data-stu-id="06af8-147">After changing hello capacity toohello desired value, hello virtual machine scale set in Azure can be updated with hello [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="06af8-148">Bir düğüm el ile eklerken, örnek bir ölçek kümesi ekleme şablon hello ölçek kümesi bu yana yeni bir Service Fabric düğümü içeren tüm bu gerekli toostart olması gerektiği gibi uzantıları tooautomatically yeni örnekleri toohello Service Fabric kümesi katılın.</span><span class="sxs-lookup"><span data-stu-id="06af8-148">As when adding a node manually, adding a scale set instance should be all that's needed toostart a new Service Fabric node since hello scale set template includes extensions tooautomatically join new instances toohello Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="06af8-149">İçinde ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="06af8-149">Scaling in</span></span>

<span data-ttu-id="06af8-150">İçinde ölçeklendirme çıkışı benzer tooscaling olur. Pratikte değişikliklerdir hello gerçek sanal makine ölçek kümesi aynı hello.</span><span class="sxs-lookup"><span data-stu-id="06af8-150">Scaling in is similar tooscaling out. hello actual virtual machine scale set changes are practically hello same.</span></span> <span data-ttu-id="06af8-151">Ancak, daha önce açıklandığı gibi Service Fabric kaldırılan düğümlerini altın veya Gümüş bir dayanıklılık yalnızca otomatik olarak temizlenir..</span><span class="sxs-lookup"><span data-stu-id="06af8-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="06af8-152">İsteğe bağlı olarak Hello Bronz dayanıklılık ölçek bileşenini durumda gerekli toointeract hello Service Fabric sahip olacak şekilde hello düğümü toobe kaldırılan aşağı tooshut ve tooremove durumuna küme.</span><span class="sxs-lookup"><span data-stu-id="06af8-152">So, in hello Bronze-durability scale-in case, it's necessary toointeract with hello Service Fabric cluster tooshut down hello node toobe removed and then tooremove its state.</span></span>

<span data-ttu-id="06af8-153">Merhaba düğümü toobe bulma kapatma içerir hello düğümü hazırlama (Merhaba en son eklenen düğümü) kaldırıldı ve onu devre dışı bırakma.</span><span class="sxs-lookup"><span data-stu-id="06af8-153">Preparing hello node for shutdown involves finding hello node toobe removed (hello most recently added node) and deactivating it.</span></span> <span data-ttu-id="06af8-154">Çekirdek olmayan düğümleri için yeni düğümler karşılaştırarak bulunabilir `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="06af8-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="06af8-155">Unutmayın, *çekirdek* düğümleri yok gibi görünüyor tooalways izleyin hello kuralı büyük örneği kimlikleri ilk kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="06af8-155">Be aware that *seed* nodes don't seem tooalways follow hello convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="06af8-156">Kaldırılan hello düğümü toobe bulunduktan sonra devre dışı bırakılabilir ve kaldırılan kullanarak, hello aynı `FabricClient` örneği ve hello `IAzure` örneğinden daha önce.</span><span class="sxs-lookup"><span data-stu-id="06af8-156">Once hello node toobe removed is found, it can be deactivated and removed using hello same `FabricClient` instance and hello `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

<span data-ttu-id="06af8-157">Komut dosyası bir yaklaşım tercih ise olarak, sanal makine ölçek değiştirmek için PowerShell cmdlet'leri ölçeğini genişletme ile kümesi kapasitesi de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="06af8-157">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="06af8-158">Merhaba sanal makine örneğini kaldırıldığında Service Fabric düğüm durumu kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="06af8-158">Once hello virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="06af8-159">Olası dezavantajları</span><span class="sxs-lookup"><span data-stu-id="06af8-159">Potential drawbacks</span></span>

<span data-ttu-id="06af8-160">Kod parçacıkları önceki hello gösterildiği gibi ölçeklendirme hizmetinizi oluşturma denetimi ve uygulamanızı üzerinden özelleştirilebilirliğini yüksek derecede hello davranışı ölçeklendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="06af8-160">As demonstrated in hello preceding code snippets, creating your own scaling service provides hello highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="06af8-161">Bu, ne zaman veya nasıl bir uygulama veya ölçeklendirir üzerinde kesin denetim gerektiren senaryolar için faydalı olabilir. Ancak, bu denetim bir kod karmaşıklığı kolaylığını ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="06af8-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="06af8-162">Bu yaklaşımı kullanarak, Önemsiz olmayan kod ölçeklendirme tooown gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="06af8-162">Using this approach means that you need tooown scaling code, which is non-trivial.</span></span>

<span data-ttu-id="06af8-163">Service Fabric ölçeklendirme nasıl ulaşmalıdır, senaryoya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="06af8-163">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="06af8-164">Ölçeklendirme seyrek hello özelliği tooadd veya kaldırma düğümleri el ile ise, muhtemelen yeterli.</span><span class="sxs-lookup"><span data-stu-id="06af8-164">If scaling is uncommon, hello ability tooadd or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="06af8-165">Daha karmaşık senaryolar için otomatik ölçeklendirme kurallarını ve hello özelliği tooscale program aracılığıyla gösterme SDK'ları güçlü alternatifleri sunar.</span><span class="sxs-lookup"><span data-stu-id="06af8-165">For more complex scenarios, auto-scale rules and SDKs exposing hello ability tooscale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06af8-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="06af8-166">Next steps</span></span>

<span data-ttu-id="06af8-167">kendi otomatik ölçeklendirme mantığı uygulamak başlatılan tooget tanıyın kendiniz ile Merhaba kavramları ve yararlı API'leri aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="06af8-167">tooget started implementing your own auto-scaling logic, familiarize yourself with hello following concepts and useful APIs:</span></span>

- [<span data-ttu-id="06af8-168">El ile veya Otomatik ölçek kurallarla ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="06af8-168">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="06af8-169">[.NET için Azure yönetim kitaplıklarını Fluent](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (bir Service Fabric kümenin temel sanal makine ölçek kümeleri ile etkileşim için yararlıdır)</span><span class="sxs-lookup"><span data-stu-id="06af8-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="06af8-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (Service Fabric kümesini ve düğümlerini ile etkileşim için yararlıdır)</span><span class="sxs-lookup"><span data-stu-id="06af8-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
