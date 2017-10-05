---
title: "Azure doku programlı ölçeklendirme hizmet | Microsoft Docs"
description: "Bir Azure Service Fabric kümesi veya ölçeklendirmek programlı olarak özel Tetikleyicileri göre"
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
ms.openlocfilehash: 46b0b62f92abbac57bc27bbcdd5821eafedf5519
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="8fdff-103">Service Fabric kümesi programlı olarak ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="8fdff-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="8fdff-104">Azure Service Fabric kümesi ölçeklendirme temellerini ele alınmıştır belgelerinde üzerinde [küme ölçeklendirme](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="8fdff-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="8fdff-105">Bu makale nasıl Service Fabric kümeleri üzerinde sanal makine ölçek kümeleri oluşturulur ve el ile veya Otomatik ölçek kurallarla Genişletilebilir kapsar.</span><span class="sxs-lookup"><span data-stu-id="8fdff-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="8fdff-106">Bu belgede daha Gelişmiş senaryolar için denetleyici Azure ölçeklendirme işlemlerinin programlama yöntemleri bakar.</span><span class="sxs-lookup"><span data-stu-id="8fdff-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="8fdff-107">Programsal ölçeklendirme nedenleri</span><span class="sxs-lookup"><span data-stu-id="8fdff-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="8fdff-108">Birçok senaryoda el ile veya Otomatik ölçek kuralı aracılığıyla ölçeklendirme iyi çözümdür.</span><span class="sxs-lookup"><span data-stu-id="8fdff-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="8fdff-109">Diğer senaryolarda, ancak bunlar sağ uygun olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-109">In other scenarios, though, they may not be the right fit.</span></span> <span data-ttu-id="8fdff-110">Bu yaklaşım olası dezavantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8fdff-110">Potential drawbacks to these approaches include:</span></span>

- <span data-ttu-id="8fdff-111">El ile ölçeklendirme oturum açın ve açıkça ölçeklendirme işlemleri istek gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-111">Manually scaling requires you to log in and explicitly request scaling operations.</span></span> <span data-ttu-id="8fdff-112">Ölçeklendirme işlemlerinin sık veya beklenmeyen zamanlarda gerekirse, bu yaklaşım iyi bir çözüm olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="8fdff-113">Otomatik ölçek kuralı sanal makine ölçek kümesindeki bir örneği kaldırdığınızda, düğüm türü Gümüş veya altın dayanıklılık düzeyini olmadıkça bunlar otomatik olarak bilgi o düğümün ilişkili Service Fabric kümesinden kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="8fdff-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from the associated Service Fabric cluster unless the node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="8fdff-114">Otomatik ölçek kuralı düzeyi Ayarla ölçekte (yerine Service Fabric düzeyinde) çalışması nedeniyle otomatik ölçek kuralı düzgün biçimde kapatılıyor olmadan Service Fabric düğümleri kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8fdff-114">Because auto-scale rules work at the scale set level (rather than at the Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="8fdff-115">Bu utangaç düğüm kaldırma 'hayalet' Service Fabric düğüm durumu ölçek bileşenini işlemlerinden sonra ardınızda.</span><span class="sxs-lookup"><span data-stu-id="8fdff-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="8fdff-116">Tek bir (veya hizmet), Service Fabric kümesindeki kaldırılmış düğüm durumu düzenli aralıklarla temizlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-116">An individual (or a service) would need to periodically clean up removed node state in the Service Fabric cluster.</span></span>
  - <span data-ttu-id="8fdff-117">Altın veya gümüş dayanıklılık düzeyine sahip bir düğüm türü otomatik olarak temizler Not düğümleri kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="8fdff-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="8fdff-118">Vardır, ancak [birçok ölçümleri](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) otomatik ölçek kuralları tarafından desteklenen, hala olduğu sınırlı bir dizi.</span><span class="sxs-lookup"><span data-stu-id="8fdff-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="8fdff-119">Senaryonuz bu kümesinde kapsanmayan bazı ölçüm göre ölçekleme için çağırırsa, otomatik ölçeklendirme kurallarını iyi bir seçenek olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="8fdff-120">Bu sınırlamalar bağlı olarak, daha özelleştirilmiş otomatik ölçekleme modelleri uygulamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8fdff-120">Based on these limitations, you may wish to implement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="8fdff-121">Ölçeklendirme API'leri</span><span class="sxs-lookup"><span data-stu-id="8fdff-121">Scaling APIs</span></span>
<span data-ttu-id="8fdff-122">Azure API hangi uygulamaların program aracılığıyla sanal makine ile çalışması için ayarlar ölçeklendirme ve Service Fabric kümeleri izin yok.</span><span class="sxs-lookup"><span data-stu-id="8fdff-122">Azure APIs exist which allow applications to programmatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="8fdff-123">Varolan otomatik ölçeklendirme seçeneği senaryonuz için işe yaramazsa, bu API'leri, özel ölçeklendirme mantığını uygulamak mümkün kılar.</span><span class="sxs-lookup"><span data-stu-id="8fdff-123">If existing auto-scale options don't work for your scenario, these APIs make it possible to implement custom scaling logic.</span></span> 

<span data-ttu-id="8fdff-124">Yeni bir durum bilgisiz hizmeti ölçeklendirme işlemlerini yönetmek için Service Fabric uygulaması eklemek için otomatik ölçeklendirme 'giriş yapılan' işlevselliği'Bu uygulama için bir yaklaşım ise.</span><span class="sxs-lookup"><span data-stu-id="8fdff-124">One approach to implementing this 'home-made' auto-scaling functionality is to add a new stateless service to the Service Fabric application to manage scaling operations.</span></span> <span data-ttu-id="8fdff-125">Hizmetin içinde `RunAsync` yöntemi, bir dizi Tetikleyicileri belirleyebilir ölçeklendirme (küme boyutu üst sınırı gibi parametreleri denetleniyor ve cooldowns ölçeklendirme dahil) gerekli olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="8fdff-125">Within the service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="8fdff-126">Sanal makine ölçek kümesi için etkileşimler (her ikisi de geçerli sanal makine örneği sayısını denetlemek ve değiştirmek için) kullanılan API [fluent yönetim Azure işlem kitaplığının](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="8fdff-126">The API used for virtual machine scale set interactions (both to check the current number of virtual machine instances and to modify it) is the [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="8fdff-127">Fluent işlem kitaplığı, sanal makine ölçek kümeleri ile etkileşmek için kullanımı kolay API sağlar.</span><span class="sxs-lookup"><span data-stu-id="8fdff-127">The fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="8fdff-128">Service Fabric kümesi etkileşim kurmak için kullanmak [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="8fdff-128">To interact with the Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="8fdff-129">Elbette, ölçekleme kod ölçeklendirilmesi için kümedeki bir hizmet olarak çalıştırmak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8fdff-129">Of course, the scaling code doesn't need to run as a service in the cluster to be scaled.</span></span> <span data-ttu-id="8fdff-130">Her ikisi de `IAzure` ve `FabricClient` ölçeklendirme hizmeti bir konsol uygulaması veya Windows hizmeti Service Fabric uygulaması dışında çalıştırma kolayca olabilir şekilde ilişkili Azure kaynaklarını uzaktan bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8fdff-130">Both `IAzure` and `FabricClient` can connect to their associated Azure resources remotely, so the scaling service could easily be a console application or Windows service running from outside the Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="8fdff-131">Kimlik bilgisi yönetimi</span><span class="sxs-lookup"><span data-stu-id="8fdff-131">Credential management</span></span>
<span data-ttu-id="8fdff-132">Ölçeklendirme işlemek için bir hizmet yazma bir hizmetin etkileşimli oturum açma olmadan sanal makine ölçek kümesi kaynaklara erişebilmeniz iştir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-132">One challenge of writing a service to handle scaling is that the service must be able to access virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="8fdff-133">Service Fabric kümesi erişme ölçeklendirme hizmeti kendi başına Service Fabric uygulaması değiştirme, ancak ölçek kümesine erişmek için kimlik bilgileri gerekli kolaydır.</span><span class="sxs-lookup"><span data-stu-id="8fdff-133">Accessing the Service Fabric cluster is easy if the scaling service is modifying its own Service Fabric application, but credentials are needed to access the scale set.</span></span> <span data-ttu-id="8fdff-134">Oturum açmak için kullanabileceğiniz bir [hizmet sorumlusu](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) ile oluşturulan [Azure CLI 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8fdff-134">To log in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with the [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="8fdff-135">Bir hizmet sorumlusu aşağıdaki adımlarla oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="8fdff-135">A service principal can be created with the following steps:</span></span>

1. <span data-ttu-id="8fdff-136">Azure CLI için oturum açma (`az login`) sanal makine ölçek erişimi olan bir kullanıcı olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="8fdff-136">Log in to the Azure CLI (`az login`) as a user with access to the virtual machine scale set</span></span>
2. <span data-ttu-id="8fdff-137">Hizmet sorumlusu ile oluşturma`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="8fdff-137">Create the service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="8fdff-138">AppID ('istemci kimliği' başka bir yerde olarak adlandırılır), adı, şifresi ve Kiracı daha sonra kullanmak için not edin.</span><span class="sxs-lookup"><span data-stu-id="8fdff-138">Make note of the appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="8fdff-139">İle görüntülenebilir abonelik Kimliğinizi de gerekir`az account list`</span><span class="sxs-lookup"><span data-stu-id="8fdff-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="8fdff-140">Fluent işlem kitaplığı gibi bu kimlik bilgilerini kullanarak oturum açabilir (çekirdek fluent Azure türleri ister Not `IAzure` bulunan [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) paket):</span><span class="sxs-lookup"><span data-stu-id="8fdff-140">The fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in the [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

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
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed to login to Azure");
}
```

<span data-ttu-id="8fdff-141">Aracılığıyla oturum açtıktan sonra ölçek kümesi örnek sayısı sorgulanabilir `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="8fdff-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="8fdff-142">Ölçeği genişletme</span><span class="sxs-lookup"><span data-stu-id="8fdff-142">Scaling out</span></span>
<span data-ttu-id="8fdff-143">İşlem SDK fluent Azure kullanarak, yalnızca birkaç aramaları ayarlamak sanal makine ölçek örnekleri eklenebilir-</span><span class="sxs-lookup"><span data-stu-id="8fdff-143">Using the fluent Azure compute SDK, instances can be added to the virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="8fdff-144">Alternatif olarak, sanal makine ölçek kümesi boyutu PowerShell cmdlet'leri ile yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="8fdff-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)sanal makine ölçek kümesi nesnesi alabilir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve the virtual machine scale set object.</span></span> <span data-ttu-id="8fdff-146">Geçerli kapasitenin depolanır `.sku.capacity` özelliği.</span><span class="sxs-lookup"><span data-stu-id="8fdff-146">The current capacity will be stored in the `.sku.capacity` property.</span></span> <span data-ttu-id="8fdff-147">İstenen değere kapasite değiştirdikten sonra sanal makineyi ölçeği Azure'da Ayarla ile güncelleştirilebilir [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) komutu.</span><span class="sxs-lookup"><span data-stu-id="8fdff-147">After changing the capacity to the desired value, the virtual machine scale set in Azure can be updated with the [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="8fdff-148">Bir düğüm el ile eklerken, örnek bir ölçek kümesi ekleme olması gerektiği gibi şablon ölçek kümesi bu yana yeni bir Service Fabric düğümü başlatmak için gerekli olan tüm otomatik olarak yeni örnekleri için Service Fabric kümesi katılmak için uzantılar içerir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-148">As when adding a node manually, adding a scale set instance should be all that's needed to start a new Service Fabric node since the scale set template includes extensions to automatically join new instances to the Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="8fdff-149">İçinde ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="8fdff-149">Scaling in</span></span>

<span data-ttu-id="8fdff-150">İçinde ölçeklendirme ölçeğini için benzer.</span><span class="sxs-lookup"><span data-stu-id="8fdff-150">Scaling in is similar to scaling out.</span></span> <span data-ttu-id="8fdff-151">Gerçek sanal makine ölçek değişiklikleri hemen hemen aynı ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8fdff-151">The actual virtual machine scale set changes are practically the same.</span></span> <span data-ttu-id="8fdff-152">Ancak, daha önce açıklandığı gibi Service Fabric kaldırılan düğümlerini altın veya Gümüş bir dayanıklılık yalnızca otomatik olarak temizlenir..</span><span class="sxs-lookup"><span data-stu-id="8fdff-152">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="8fdff-153">Bu nedenle Bronz dayanıklılık ölçek bileşenini durumunda kaldırılacak düğümü kapatılacağını Service Fabric kümesi ile etkileşim kurmak ise gerekli ardından durumuna kaldırmak için.</span><span class="sxs-lookup"><span data-stu-id="8fdff-153">So, in the Bronze-durability scale-in case, it's necessary to interact with the Service Fabric cluster to shut down the node to be removed and then to remove its state.</span></span>

<span data-ttu-id="8fdff-154">Düğümü için kapatma hazırlanıyor (en son eklenen düğüm) düğümü kaldırılan bulunmasını ve devre dışı bırakmadan içerir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-154">Preparing the node for shutdown involves finding the node to be removed (the most recently added node) and deactivating it.</span></span> <span data-ttu-id="8fdff-155">Çekirdek olmayan düğümleri için yeni düğümler karşılaştırarak bulunabilir `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="8fdff-155">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="8fdff-156">Unutmayın, *çekirdek* düğümleri olmayan gözükmüyor her zaman büyük örneği kimlikleri ilk kaldırılır kuralını izler.</span><span class="sxs-lookup"><span data-stu-id="8fdff-156">Be aware that *seed* nodes don't seem to always follow the convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="8fdff-157">Kaldırılacak düğüm bulunduktan sonra devre dışı bırakılabilir ve aynı kullanarak kaldırılan `FabricClient` örneği ve `IAzure` örneğinden daha önce.</span><span class="sxs-lookup"><span data-stu-id="8fdff-157">Once the node to be removed is found, it can be deactivated and removed using the same `FabricClient` instance and the `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove the node from the Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up to a timeout) for the node to gracefully shutdown
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

<span data-ttu-id="8fdff-158">Komut dosyası bir yaklaşım tercih ise olarak, sanal makine ölçek değiştirmek için PowerShell cmdlet'leri ölçeğini genişletme ile kümesi kapasitesi de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-158">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="8fdff-159">Sanal makine örneğini kaldırıldığında Service Fabric düğüm durumu kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-159">Once the virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="8fdff-160">Olası dezavantajları</span><span class="sxs-lookup"><span data-stu-id="8fdff-160">Potential drawbacks</span></span>

<span data-ttu-id="8fdff-161">Önceki kod parçacıkları gösterildiği gibi kendi hizmet ölçeklendirme oluşturmak en yüksek derecede denetim ve uygulamanızı üzerinden özelleştirilebilirliğini davranışı ölçeklendirme kullanıcının sağlar.</span><span class="sxs-lookup"><span data-stu-id="8fdff-161">As demonstrated in the preceding code snippets, creating your own scaling service provides the highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="8fdff-162">Bu, ne zaman veya nasıl bir uygulama veya ölçeklendirir üzerinde kesin denetim gerektiren senaryolar için faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-162">This can be useful for scenarios requiring precise control over when or how an application scales in or out.</span></span> <span data-ttu-id="8fdff-163">Ancak, bu denetim bir kod karmaşıklığı kolaylığını ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-163">However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="8fdff-164">Bu yaklaşımı kullanarak, Önemsiz olmayan olan kendi ölçeklendirme kod, gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8fdff-164">Using this approach means that you need to own scaling code, which is non-trivial.</span></span>

<span data-ttu-id="8fdff-165">Service Fabric ölçeklendirme nasıl ulaşmalıdır, senaryoya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8fdff-165">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="8fdff-166">Ölçeklendirme seyrek ise, ekleme veya düğümleri el ile kaldırma yeteneği büyük olasılıkla yeterli olur.</span><span class="sxs-lookup"><span data-stu-id="8fdff-166">If scaling is uncommon, the ability to add or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="8fdff-167">Daha karmaşık senaryolar için otomatik ölçeklendirme kurallarını ve SDK'ları ölçeklendirmenizi program aracılığıyla gösterme güçlü alternatifleri sunar.</span><span class="sxs-lookup"><span data-stu-id="8fdff-167">For more complex scenarios, auto-scale rules and SDKs exposing the ability to scale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fdff-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8fdff-168">Next steps</span></span>

<span data-ttu-id="8fdff-169">Kendi otomatik ölçeklendirme mantığı uygulamak başlamak için aşağıdaki kavramlar ve yararlı API'leri ile edinin:</span><span class="sxs-lookup"><span data-stu-id="8fdff-169">To get started implementing your own auto-scaling logic, familiarize yourself with the following concepts and useful APIs:</span></span>

- [<span data-ttu-id="8fdff-170">El ile veya Otomatik ölçek kurallarla ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="8fdff-170">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="8fdff-171">[.NET için Azure yönetim kitaplıklarını Fluent](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (bir Service Fabric kümenin temel sanal makine ölçek kümeleri ile etkileşim için yararlıdır)</span><span class="sxs-lookup"><span data-stu-id="8fdff-171">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="8fdff-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (Service Fabric kümesini ve düğümlerini ile etkileşim için yararlıdır)</span><span class="sxs-lookup"><span data-stu-id="8fdff-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
