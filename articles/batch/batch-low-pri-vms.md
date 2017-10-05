---
title: "Düşük maliyetli düşük öncelikli sanal makinelerin (Önizleme) Azure Batch iş yüklerini çalıştırmak | Microsoft Docs"
description: "Düşük öncelikli sanal makineleri Azure Batch iş yükü maliyetini azaltmak için hazırlamayı öğrenin."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 9bf0ac322020d8a8453011c3207c1930175db6d3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="b72df-103">Düşük öncelikli sanal makineleri toplu (Önizleme) ile kullanma</span><span class="sxs-lookup"><span data-stu-id="b72df-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="b72df-104">Azure Batch düşük versiyonda öncelik sanal makineleri (VM'ler) Batch iş yükü maliyetini azaltmak için sunar.</span><span class="sxs-lookup"><span data-stu-id="b72df-104">Azure Batch offers low-priorty virtual machines (VMs) to reduce the cost of Batch workloads.</span></span> <span data-ttu-id="b72df-105">Düşük öncelikli sanal makineleri de ekonomiktir işlem gücü, büyük bir miktarını sağlayarak, toplu iş yüklerinin yeni türleri mümkün kılar.</span><span class="sxs-lookup"><span data-stu-id="b72df-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="b72df-106">Düşük öncelikli sanal makineleri Azure'da fazlalık kapasite yararlanın.</span><span class="sxs-lookup"><span data-stu-id="b72df-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="b72df-107">Düşük öncelikli sanal makineleri, havuzlarınızı belirttiğinizde, Azure Batch bu fazlalık kullanılabilir olduğunda otomatik olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b72df-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="b72df-108">Düşük öncelikli sanal makineleri kullanma kolaylığını hiçbir fazlalık kapasite Azure içinde kullanılabilir olduğunda bu VM'lerin etkisiz ' dir.</span><span class="sxs-lookup"><span data-stu-id="b72df-108">The tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="b72df-109">Bu nedenle, düşük öncelikli sanal makineleri belirli türde bir iş yükleri için en uygun.</span><span class="sxs-lookup"><span data-stu-id="b72df-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="b72df-110">Düşük öncelikli sanal makineleri toplu ve burada iş tamamlanma zamanı esnek ve iş üzerinde birçok VM dağıtılmış zaman uyumsuz işleme iş yükleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="b72df-110">Use low-priority VMs for batch and asynchronous processing workloads where the job completion time is flexible and the work is distributed across many VMs.</span></span>

<span data-ttu-id="b72df-111">Düşük öncelikli sanal makineleri özel VM'ler önemli ölçüde daha az pahalıdır.</span><span class="sxs-lookup"><span data-stu-id="b72df-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="b72df-112">Fiyatlandırma ayrıntıları için bkz: [Batch fiyatlandırması](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="b72df-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="b72df-113">Düşük öncelikli sanal makineleri için bir ek tartışma blog yayını duyurusuna bakın: [toplu bir fiyat kesir bilgi işlem](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span><span class="sxs-lookup"><span data-stu-id="b72df-113">For an additional discussion of low-priority VMs, see the blog post announcement: [Batch computing at a fraction of the price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b72df-114">Düşük öncelikli sanal makineleri şu anda önizlemede ve yalnızca toplu işlemde çalışan iş yükleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b72df-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="b72df-115">Düşük öncelikli VM'ler için kullanım örnekleri</span><span class="sxs-lookup"><span data-stu-id="b72df-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="b72df-116">Düşük öncelikli sanal makineleri, hangi iş yüklerini kullanabilir ve bunları kullanamazsınız özelliklerini verilen?</span><span class="sxs-lookup"><span data-stu-id="b72df-116">Given the characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="b72df-117">Genel olarak, işleri birçok paralel görevlere bozuk veya çıkışı ölçeği ve üzerinde birçok VM dağıtılan birçok iş iyi bir tercihtir toplu işleme iş yüklerinin olduğunu.</span><span class="sxs-lookup"><span data-stu-id="b72df-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="b72df-118">Azure fazlalık kapasite kullanımını en üst düzeye çıkarmak için kullanıma uygun işleri ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b72df-118">To maximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="b72df-119">Bazen VM'ler kullanılabilir durumda olmayabilir veya, işleri için sınırlı kapasite neden olur ve görev kesinti ve tekrar bölümlerini etkisiz.</span><span class="sxs-lookup"><span data-stu-id="b72df-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead to task interruption and reruns.</span></span> <span data-ttu-id="b72df-120">Bu nedenle işlerini çalıştırmak için uygulayabileceğiniz zamanında esnek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b72df-120">Jobs must therefore be flexible in the time they can take to run.</span></span>

-   <span data-ttu-id="b72df-121">İşlerini uzun görevlerle kesintiye varsa daha etkilenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="b72df-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="b72df-122">Uzun süre çalışan görevlerini bunlar yürütmek olarak ilerleme durumunu kaydetmek için denetim noktası oluşturma uygulama ise, ardından kesinti etkisini çok daha az olabilir.</span><span class="sxs-lookup"><span data-stu-id="b72df-122">If long-running tasks implement checkpointing to save progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="b72df-123">Kısa yürütme süreleri görevlerle kesinti etkisini çok daha az olduğu gibi düşük öncelikli sanal makineleri ile en iyi şekilde çalışır eğilimindedir.</span><span class="sxs-lookup"><span data-stu-id="b72df-123">Tasks with shorter execution times tend to work best with low-priority VMs as the impact of interruption is far less.</span></span>

-   <span data-ttu-id="b72df-124">Uzun süre çalışan birden çok VM kullanan MPI işlerini uygun değildir düşük öncelikli sanal makineleri bir VM etkisiz olarak kullanmak için büyük olasılıkla yeniden çalıştırılması gerek kalmadan tüm iş götürür.</span><span class="sxs-lookup"><span data-stu-id="b72df-124">Long-running MPI jobs that utilize multiple VMs are not well suited to use low-priority VMs as one preempted VM will likely lead to the whole job having to be run again.</span></span>

<span data-ttu-id="b72df-125">Düşük öncelikli sanal makineleri kullanmak için uygun toplu işleme kullanım örnekleri iyi bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b72df-125">Some examples of batch processing use cases well suited to use low-priority VMs are:</span></span>

-   <span data-ttu-id="b72df-126">**Geliştirme ve test**: özel olarak, büyük ölçekli çözümleri geliştirdiğinizde, önemli tasarrufları alırlar.</span><span class="sxs-lookup"><span data-stu-id="b72df-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="b72df-127">Sınama tüm türleri yararlanabilirsiniz, ancak büyük ölçekli yük test etme ve gerileme sınaması harika kullanır.</span><span class="sxs-lookup"><span data-stu-id="b72df-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="b72df-128">**İsteğe bağlı kapasite ekleme**: düşük öncelikli sanal makineleri, normal özel VM'ler - tamamlamak için kullanılabilir kullanılabilir olduğunda, işleri ölçeklendirmek ve bu nedenle daha hızlı tamamlamak için daha düşük maliyetli; mevcut değil, özel VM'ler temel alındığında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b72df-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, the baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="b72df-129">**Esnek iş yürütme süresi**: varsa zaman işler esnekliğe sahip tamamlamak daha sonra kapasite olası bırakmaları izin; ancak, düşük öncelikli sanal makineleri eklenmesiyle işleri sık daha hızlı ve daha düşük maliyetli bir çalışır.</span><span class="sxs-lookup"><span data-stu-id="b72df-129">**Flexible job execution time**: If there is flexibility in the time jobs have to complete, then potential drops in capacity can be tolerated; however, with the addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="b72df-130">Batch havuzları, iş yürütme süresi esneklik bağlı olarak birkaç şekilde düşük öncelikli sanal makineleri kullanmak üzere yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="b72df-130">Batch pools can be configured to use low-priority VMs in a few ways, depending on the flexibility in job execution time:</span></span>

-   <span data-ttu-id="b72df-131">Düşük öncelikli sanal makineleri yalnızca bir havuzda kullanılabilir ve toplu herhangi preempted kapasite kullanılabilir olduğunda yalnızca kurtarır.</span><span class="sxs-lookup"><span data-stu-id="b72df-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="b72df-132">Düşük öncelikli yalnızca VM'ler kullanılır işleri yürütmek üzere ucuz yoludur.</span><span class="sxs-lookup"><span data-stu-id="b72df-132">This is the cheapest way to execute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="b72df-133">Düşük öncelikli sanal makineleri, sabit bir taban çizgisi özel VM'ler ile birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b72df-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="b72df-134">Ayrılmış sanal sabit sayıda her zaman bir iş İleri aşamalara tutmak için bazı kapasite olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="b72df-134">The fixed number of dedicated VMs ensures there is always some capacity to keep a job progressing.</span></span>

-   <span data-ttu-id="b72df-135">Böylece cheaper düşük öncelikli VM'ler kullanılabilir olduğunda yalnızca kullanılan ayrılmış ve düşük öncelikli sanal makineleri, dinamik karışımını olabilir, ancak tam fiyatlı özel VM'ler gerektiğinde İleri aşamalara işleri tutmak kullanılabilir kapasite en düşük düzeyde tutmak için ölçeklenir.</span><span class="sxs-lookup"><span data-stu-id="b72df-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but the full-priced dedicated VMs are scaled up when required, to keep a minimum amount of capacity available to keep the jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="b72df-136">Düşük öncelikli VM'ler için toplu desteği</span><span class="sxs-lookup"><span data-stu-id="b72df-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="b72df-137">Azure toplu işlem kullanmasına ve düşük öncelikli Vm'lerden yararlanmak kolaylaştıran çeşitli özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="b72df-137">Azure Batch provides several capabilities that make it easy to consume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="b72df-138">Batch havuzları özel VM'ler ve düşük öncelikli sanal makineleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="b72df-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="b72df-139">Bir havuzu oluşturulduğunda veya açık yeniden boyutlandırma işlemi veya Otomatik ölçek kullanarak mevcut bir havuz için herhangi bir zamanda değiştirildi VM türlerinin sayısı belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="b72df-139">The number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using the explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="b72df-140">İş ve görev gönderimi değişmeden kalır ve havuzdaki VM türleriyle endişelenmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b72df-140">Job and task submission can remain unchanged and do not need to be concerned with the VM types in the pool.</span></span> <span data-ttu-id="b72df-141">Tamamen kapasite çalışan işleri korumak için en düşük eşiğin altına düşerse işlerini mümkün, ancak özel VM'ler yukarı döndürme olarak ailenin çalıştırmak için düşük öncelikli sanal makineleri kullanmak bir havuzu olması mümkündür.</span><span class="sxs-lookup"><span data-stu-id="b72df-141">It is also possible to have a pool completely use low-priority VMs to run jobs as cheaply as possible, but spin up dedicated VMs if the capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="b72df-142">Batch havuzlarının otomatik olarak düşük öncelikli VM'ler hedef sayısını arama.</span><span class="sxs-lookup"><span data-stu-id="b72df-142">Batch pools automatically seek to the target number of low-priority VMs.</span></span> <span data-ttu-id="b72df-143">Sanal makineleri etkisiz, toplu kayıp kapasite değiştirin ve hedef dönmek deneyecek.</span><span class="sxs-lookup"><span data-stu-id="b72df-143">If VMs are preempted, then Batch will attempt to replace the lost capacity and return to the target.</span></span>

-   <span data-ttu-id="b72df-144">Kesintiye görevleri olması durumunda toplu algılar ve otomatik olarak yeniden çalıştırılacak görevleri disablecomputenodeschedulingoption.</span><span class="sxs-lookup"><span data-stu-id="b72df-144">In the case of tasks being interrupted, Batch will detect and automatically requeue tasks to be run again.</span></span>

-   <span data-ttu-id="b72df-145">Düşük öncelikli sanal makineleri özel VM'ler farklı bir çekirdek kotası var.</span><span class="sxs-lookup"><span data-stu-id="b72df-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="b72df-146">Düşük öncelikli sanal makineleri daha az maliyet olduğundan düşük öncelikli sanal makineleri için bir teklif, özel VM'ler, yüksektir.</span><span class="sxs-lookup"><span data-stu-id="b72df-146">The quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="b72df-147">Bkz: [Batch Hizmeti kotaları ve sınırlarına](batch-quota-limit.md#resource-quotas) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b72df-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="b72df-148">Düşük öncelikli sanal makineleri şu anda desteklenmemektedir için havuzu ayırma modu ayarlandığı Batch hesaplarıyla ilgili [kullanıcı aboneliği](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="b72df-148">Low-priority VMs are not currently supported for Batch accounts where the pool allocation mode is set to [User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="b72df-149">Oluşturma ve havuzları güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b72df-149">Create and update pools</span></span>

<span data-ttu-id="b72df-150">Batch havuzundaki (işlem düğümleri olarak da bilinir) hem adanmış hem de düşük öncelikli sanal makineleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="b72df-150">A Batch pool can contain both dedicated and low-priority VMs (also referred to as compute nodes).</span></span> <span data-ttu-id="b72df-151">Hem özel hem de düşük öncelikli VM'ler için işlem düğümleri sayısını ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b72df-151">You can set the target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="b72df-152">Düğümlerin hedef sayısını havuzunda olmasını istediğiniz VM'lerin sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b72df-152">The target number of nodes specifies the number of VMs you want to have in the pool.</span></span>

<span data-ttu-id="b72df-153">Örneğin, bir havuzu oluşturmak için Azure bulut hizmeti VM'ler 5 hedefle kullanarak sanal makineleri ve 20 düşük öncelikli sanal makineleri ayrılmış:</span><span class="sxs-lookup"><span data-stu-id="b72df-153">For example, to create a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="b72df-154">Bir havuzu oluşturmak için 5'in bir hedef Azure sanal makineleri (Bu durumda Linux VM'ler) kullanarak sanal makineleri ve 20 düşük öncelikli sanal makineleri ayrılmış:</span><span class="sxs-lookup"><span data-stu-id="b72df-154">To create a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="b72df-155">Geçerli düğüm sayısını hem adanmış hem de düşük öncelikli VM'ler için alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b72df-155">You can get the current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="b72df-156">Havuz düğümleri düğüm adanmış veya düşük öncelikli bir VM olup olmadığını gösteren bir özelliği vardır:</span><span class="sxs-lookup"><span data-stu-id="b72df-156">Pool nodes have a property to indicate if the node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="b72df-157">Bir veya daha fazla düğüm havuzunda etkisiz, havuzu üzerinde bir liste düğümleri işlemi hala düğümleri döndürür, düşük öncelikli düğüm geçerli sayısını değişmeden kalır, ancak bu düğümler kümesine durumlarına sahip olur **geçersiz kılındı** durumu.</span><span class="sxs-lookup"><span data-stu-id="b72df-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, the current number of low-priority nodes will remain unchanged, but those nodes will have their state set to the **Preempted** state.</span></span> <span data-ttu-id="b72df-158">Toplu değiştirme sanal makineleri Bul deneyecek ve düğümlerin Git başarılı olursa, **oluşturma** ve ardından **başlangıç** durumları görev yürütme için kullanılabilir hale gelmeden önce olduğu gibi yeni düğümler.</span><span class="sxs-lookup"><span data-stu-id="b72df-158">Batch will attempt to find replacement VMs and, if successful, the nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="b72df-159">Düşük öncelikli sanal makineleri içeren bir havuzu ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="b72df-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="b72df-160">Yalnızca özel VM'ler oluşan havuzlarıyla gibi düşük öncelikli sanal makineleri otomatik ölçek kullanarak veya yeniden boyutlandırma yöntemini çağırarak içeren bir havuzu ölçeklendirmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="b72df-160">As with pools solely consisting of dedicated VMs, it is possible to scale a pool containing low-priority VMs by calling the Resize method or by using auto-scale.</span></span>

<span data-ttu-id="b72df-161">Havuzu yeniden boyutlandırma işlemi değerini güncelleştirmeleri ikinci bir isteğe bağlı parametresi alan **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="b72df-161">The pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="b72df-162">Havuz otomatik ölçeklendirme formülü aşağıdaki gibi düşük öncelikli sanal makineleri destekler:</span><span class="sxs-lookup"><span data-stu-id="b72df-162">The pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="b72df-163">Almak veya hizmet tanımlı değişkenin değerini ayarlamak **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="b72df-163">You can get or set the value of the service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="b72df-164">Hizmet tanımlı değişkenin değerini alabilir **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="b72df-164">You can get the value of the service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="b72df-165">Hizmet tanımlı değişkenin değerini alabilir **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="b72df-165">You can get the value of the service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="b72df-166">Bu değişken preempted durumda düğümlerin sayısını döndürür ve yukarı veya aşağı kullanılamaz etkisiz düğüm sayısına bağlı olarak ayrılmış düğüm sayısını ölçeklendirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b72df-166">This variable returns the number of nodes in the preempted state and allows you to scale up or down the number of dedicated nodes, depending on the number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="b72df-167">İşler ve görevler</span><span class="sxs-lookup"><span data-stu-id="b72df-167">Jobs and tasks</span></span>

<span data-ttu-id="b72df-168">İşlerini ve görevleri düşük önceliğe düğümleri için çok az desteği gerektirir; yalnızca desteği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b72df-168">Jobs and tasks require very little support for low-priority nodes; the only support is as follows:</span></span>

-   <span data-ttu-id="b72df-169">Yeni bir özellik JobManagerTask özelliğinin bir işin **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="b72df-169">The JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="b72df-170">Bu özelliği true olduğunda, iş yöneticisi görevi ya da bir adanmış veya düşük öncelikli düğümünde zamanlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b72df-170">When this property is true, the job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="b72df-171">Bu özellik false ise, iş yöneticisi görevi yalnızca adanmış bir düğüme zamanlanacak.</span><span class="sxs-lookup"><span data-stu-id="b72df-171">If this property is false, the job manager task will be scheduled to a dedicated node only.</span></span>

-   <span data-ttu-id="b72df-172">Bir [ortam değişkeni](batch-compute-node-environment-variables.md) düşük öncelikli veya ayrılmış bir düğümde çalışan olup olmadığını belirleyebilmek görev uygulamaları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b72df-172">An [environment variable](batch-compute-node-environment-variables.md) is available to a task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="b72df-173">AZ_BATCH_NODE_IS_DEDICATED ortam değişkenidir.</span><span class="sxs-lookup"><span data-stu-id="b72df-173">The environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="b72df-174">Önalım işleme</span><span class="sxs-lookup"><span data-stu-id="b72df-174">Handling preemption</span></span>

<span data-ttu-id="b72df-175">Sanal makineleri bazen etkisiz; Bu gerçekleştiğinde, toplu şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="b72df-175">VMs may occasionally be preempted; when this happens, Batch does the following:</span></span>

-   <span data-ttu-id="b72df-176">Preempted VM'ler için güncelleştirilmiş durumlarına sahip **geçersiz kılındı**.</span><span class="sxs-lookup"><span data-stu-id="b72df-176">The preempted VMs have their state updated to **Preempted**.</span></span>
-   <span data-ttu-id="b72df-177">Görevler etkisiz düğümü Vm'lerde çalışıyordu, ardından bu görevleri yeniden kuyruğa ve yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b72df-177">If tasks were running on the preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="b72df-178">VM etkili bir şekilde silindi kaybolmasına VM üzerinde yerel olarak depolanan tüm verileri önde gelen.</span><span class="sxs-lookup"><span data-stu-id="b72df-178">The VM is effectively deleted, leading to any data stored locally on the VM being lost.</span></span>
-   <span data-ttu-id="b72df-179">Havuz sürekli olarak kullanılabilir düşük öncelikli düğümlerin hedef sayısını ulaşmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b72df-179">The pool continually attempts to reach the target number of low-priority nodes available.</span></span> <span data-ttu-id="b72df-180">Yedek kapasite bulunduğunda, düğümlerin kimlikleri tutmak ancak, oluşturulmak yeniden başlatılır **oluşturma** ve **başlangıç** görev zamanlama için kullanılabilir önce belirtir.</span><span class="sxs-lookup"><span data-stu-id="b72df-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="b72df-181">Önalım sayıları, Azure portalında bir ölçü olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b72df-181">Preemption counts are available as a metric in the Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="b72df-182">Ölçümler</span><span class="sxs-lookup"><span data-stu-id="b72df-182">Metrics</span></span>

<span data-ttu-id="b72df-183">Yeni ölçümleri kullanılabilir [Azure portal](https://portal.azure.com) düşük öncelikli düğümleri için.</span><span class="sxs-lookup"><span data-stu-id="b72df-183">New metrics are available in the [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="b72df-184">Bu ölçümler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b72df-184">These metrics are:</span></span>

- <span data-ttu-id="b72df-185">Düşük öncelikli düğüm sayısı</span><span class="sxs-lookup"><span data-stu-id="b72df-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="b72df-186">Düşük öncelikli çekirdek sayısı</span><span class="sxs-lookup"><span data-stu-id="b72df-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="b72df-187">Etkisiz düğüm sayısı</span><span class="sxs-lookup"><span data-stu-id="b72df-187">Preempted Node Count</span></span>

<span data-ttu-id="b72df-188">Azure Portal'da ölçümleri görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="b72df-188">To view metrics in the Azure portal:</span></span>

1. <span data-ttu-id="b72df-189">Portalda Batch hesabınıza gidin ve toplu işlem hesabı için ayarları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="b72df-189">Navigate to your Batch account in the portal, and view the settings for your Batch account.</span></span>
2. <span data-ttu-id="b72df-190">Seçin **ölçümleri** gelen **izleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="b72df-190">Select **Metrics** from the **Monitoring** section.</span></span>
3. <span data-ttu-id="b72df-191">İşlemleriniz ölçümleri seçin **kullanılabilir ölçümler** listesi.</span><span class="sxs-lookup"><span data-stu-id="b72df-191">Select the metrics you desire from the **Available Metrics** list.</span></span>

![Düşük öncelikli düğümleri için ölçümleri](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="b72df-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b72df-193">Next steps</span></span>

* <span data-ttu-id="b72df-194">Batch kullanmaya hazırlanan herkes için gerekli bilgileri içeren [Geliştiriciler için Batch özelliğine genel bakış](batch-api-basics.md) konusunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="b72df-194">Read the [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing to use Batch.</span></span> <span data-ttu-id="b72df-195">Bu makalede havuzlar, düğümler, işler ve görevler gibi Batch hizmet kaynakları ve Batch uygulamanızı oluştururken kullanabileceğiniz birçok API özelliği hakkında daha ayrıntılı bilgi verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b72df-195">The article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and the many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="b72df-196">Batch çözümleri oluşturmak için kullanılabilen [Batch API’leri ve araçları](batch-apis-tools.md) hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="b72df-196">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
