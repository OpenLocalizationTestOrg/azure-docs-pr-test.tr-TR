---
title: "Küme Kaynak Yöneticisi küme açıklaması | Microsoft Docs"
description: "Service Fabric kümesi, hata etki alanlarını, yükseltme etki alanları, düğüm özellikleri ve düğüm kapasitesi için Küme Kaynak Yöneticisi'ni belirterek açıklayan."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: e517eda4d3ff7ad81998003688c3cca78f76e179
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="describing-a-service-fabric-cluster"></a><span data-ttu-id="7d03d-103">Service fabric kümesi açıklayan</span><span class="sxs-lookup"><span data-stu-id="7d03d-103">Describing a service fabric cluster</span></span>
<span data-ttu-id="7d03d-104">Service Fabric kümesi Kaynak Yöneticisi, bir küme açıklamak için çeşitli mekanizmalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d03d-104">The Service Fabric Cluster Resource Manager provides several mechanisms for describing a cluster.</span></span> <span data-ttu-id="7d03d-105">Çalışma zamanı sırasında Küme Kaynak Yöneticisi'ni kümede çalışan hizmetler yüksek düzeyde kullanılabilirliğini sağlamak için bu bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-105">During runtime, the Cluster Resource Manager uses this information to ensure high availability of the services running in the cluster.</span></span> <span data-ttu-id="7d03d-106">Bu önemli kurallar zorlarken bu aynı zamanda kümedeki kaynak tüketimini en iyi duruma dener.</span><span class="sxs-lookup"><span data-stu-id="7d03d-106">While enforcing these important rules, it also attempts to optimize the resource consumption within the cluster.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="7d03d-107">Önemli kavramlar</span><span class="sxs-lookup"><span data-stu-id="7d03d-107">Key concepts</span></span>
<span data-ttu-id="7d03d-108">Küme Kaynak Yöneticisi'ni bir küme açıklayan çeşitli özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="7d03d-108">The Cluster Resource Manager supports several features that describe a cluster:</span></span>

* <span data-ttu-id="7d03d-109">Hata etki alanları</span><span class="sxs-lookup"><span data-stu-id="7d03d-109">Fault Domains</span></span>
* <span data-ttu-id="7d03d-110">Yükseltme etki alanları</span><span class="sxs-lookup"><span data-stu-id="7d03d-110">Upgrade Domains</span></span>
* <span data-ttu-id="7d03d-111">Düğüm özellikleri</span><span class="sxs-lookup"><span data-stu-id="7d03d-111">Node Properties</span></span>
* <span data-ttu-id="7d03d-112">Düğüm kapasitesi</span><span class="sxs-lookup"><span data-stu-id="7d03d-112">Node Capacities</span></span>

## <a name="fault-domains"></a><span data-ttu-id="7d03d-113">Hata etki alanları</span><span class="sxs-lookup"><span data-stu-id="7d03d-113">Fault domains</span></span>
<span data-ttu-id="7d03d-114">Hata etki alanı herhangi Eşgüdümlü hatası alanıdır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-114">A Fault Domain is any area of coordinated failure.</span></span> <span data-ttu-id="7d03d-115">(Sürücü hatalara bozuk NIC bellenimi için güç kaynağı hatalardan için kendi çeşitli nedenlerle üzerinde başarısız olacağından bu yana) tek bir makineye bir hata etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-115">A single machine is a Fault Domain (since it can fail on its own for various reasons, from power supply failures to drive failures to bad NIC firmware).</span></span> <span data-ttu-id="7d03d-116">Elektrik kesintisinden veya tek bir konumda tek bir kaynak paylaşımı makineler olduğu gibi aynı Ethernet anahtara bağlı makine aynı hata etki alanında yok.</span><span class="sxs-lookup"><span data-stu-id="7d03d-116">Machines connected to the same Ethernet switch are in the same Fault Domain, as are machines sharing a single source of power or in a single location.</span></span> <span data-ttu-id="7d03d-117">Donanım hatalarının çakışmasına doğal olduğundan, hata etki alanlarını kendiliğinden hiyerarşik ve Service Fabric URI'ler olarak temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-117">Since it's natural for hardware faults to overlap, Fault Domains are inherently hierarchal and are represented as URIs in Service Fabric.</span></span>

<span data-ttu-id="7d03d-118">Service Fabric güvenle Hizmetleri yerleştirmek için bu bilgileri kullandığından hata etki alanlarının doğru şekilde ayarlandığından emin önemlidir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-118">It is important that Fault Domains are set up correctly since Service Fabric uses this information to safely place services.</span></span> <span data-ttu-id="7d03d-119">Service Fabric Git bir hizmet hata (bazı bileşeninin hatadan kaynaklanıyor) etki alanı kaybedilmesine neden olacağı şekilde Hizmetleri yerleştirmek istediğiniz değil.</span><span class="sxs-lookup"><span data-stu-id="7d03d-119">Service Fabric doesn't want to place services such that the loss of a Fault Domain (caused by the failure of some component) causes a service to go down.</span></span> <span data-ttu-id="7d03d-120">Azure ortamı Service Fabric ortamı tarafından sağlanan hata etki alanı bilgileri doğru sizin adınıza kümedeki düğümleri yapılandırmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-120">In the Azure environment Service Fabric uses the Fault Domain information provided by the environment to correctly configure the nodes in the cluster on your behalf.</span></span> <span data-ttu-id="7d03d-121">Küme ayarlama zaman tanımlanan için Service Fabric tek başına, hata etki alanları</span><span class="sxs-lookup"><span data-stu-id="7d03d-121">For Service Fabric Standalone, Fault Domains are defined at the time that the cluster is set up</span></span> 

> [!WARNING]
> <span data-ttu-id="7d03d-122">Service Fabric sağlanan hata etki alanı bilgileri doğru olması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-122">It is important that the Fault Domain information provided to Service Fabric is accurate.</span></span> <span data-ttu-id="7d03d-123">Örneğin, Service Fabric kümenin düğümleri beş fiziksel ana bilgisayarda çalışan 10 sanal makinelerde çalıştırılan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="7d03d-123">For example, let's say that your Service Fabric cluster's nodes are running inside 10 virtual machines, running on five physical hosts.</span></span> <span data-ttu-id="7d03d-124">Bu durumda, olsa bile 10 sanal makineyi, var. yalnızca 5 farklı (üst düzey) hata etki alanları.</span><span class="sxs-lookup"><span data-stu-id="7d03d-124">In this case, even though there are 10 virtual machines, there's only 5 different (top level) fault domains.</span></span> <span data-ttu-id="7d03d-125">Aynı fiziksel ana bilgisayar paylaşımı fiziksel ana bilgisayarları başarısız olursa VM'ler Eşgüdümlü hatasıyla karşılaşan beri aynı kök hata etki paylaşmak VM'ler neden olur.</span><span class="sxs-lookup"><span data-stu-id="7d03d-125">Sharing the same physical host causes VMs to share the same root fault domain, since the VMs experience coordinated failure if their physical host fails.</span></span>  
>
> <span data-ttu-id="7d03d-126">Service Fabric hata etki alanı değil değiştirmek için bir düğümün bekliyor beri.</span><span class="sxs-lookup"><span data-stu-id="7d03d-126">Since Service Fabric expects the Fault Domain of a node not to change.</span></span> <span data-ttu-id="7d03d-127">Sanal makineleri yüksek kullanılabilirliği gibi sağlamaya başka mekanizmalar [HA-VMs](https://technet.microsoft.com/en-us/library/cc967323.aspx), saydam VM'ler geçişini bir ana bilgisayardan diğerine kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d03d-127">Other mechanisms of ensuring high availability of the VMs, such as [HA-VMs](https://technet.microsoft.com/en-us/library/cc967323.aspx), use transparent migration of VMs from one host to another.</span></span> <span data-ttu-id="7d03d-128">Bu mekanizmaların etmeyin yeniden yapılandırın veya VM içinde çalışan kod bildirin.</span><span class="sxs-lookup"><span data-stu-id="7d03d-128">These mechanisms do not reconfigure or notify the running code inside the VM.</span></span> <span data-ttu-id="7d03d-129">Bu nedenle, oldukları **desteklenmiyor** Service Fabric çalıştırmak için ortam olarak kümeleri.</span><span class="sxs-lookup"><span data-stu-id="7d03d-129">As such, they are **not supported** as environments for running Service Fabric clusters.</span></span> <span data-ttu-id="7d03d-130">Service Fabric işe yalnızca yüksek oranda kullanılabilirlik teknolojisi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-130">Service Fabric should be the only high-availability technology employed.</span></span> <span data-ttu-id="7d03d-131">Dinamik VM geçiş gibi mekanizmaları SAN'lar, veya diğerleri gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-131">Mechanisms like live VM migration, SANs, or others are not necessary.</span></span> <span data-ttu-id="7d03d-132">Service Fabric, bu mekanizmaların ile birlikte kullandıysanız _azaltmak_ uygulama kullanılabilirliği ve güvenilirliği ek karmaşıklık tanıtmak için hata merkezi kaynakları ekleyin ve güvenilirlik kullanma ve Service Fabric de çakışan kullanılabilirlik stratejisi.</span><span class="sxs-lookup"><span data-stu-id="7d03d-132">If used in conjunction with Service Fabric, these mechanisms _reduce_ application availability and reliability because they introduce additional complexity, add centralized sources of failure, and utilize reliability and availability strategies that conflict with those in Service Fabric.</span></span> 
>
>

<span data-ttu-id="7d03d-133">Aşağıdaki grafikte hata etki alanları için katkıda ve tüm farklı hataya neden etki alanlarını listelemek tüm varlıklar rengi.</span><span class="sxs-lookup"><span data-stu-id="7d03d-133">In the graphic below we color all the entities that contribute to Fault Domains and list all the different Fault Domains that result.</span></span> <span data-ttu-id="7d03d-134">Bu örnekte, veri merkezleri ("DC"), kabin ("R") ve dikey pencerelerde ("B") sahip.</span><span class="sxs-lookup"><span data-stu-id="7d03d-134">In this example, we have datacenters ("DC"), racks ("R"), and blades ("B").</span></span> <span data-ttu-id="7d03d-135">Alanlara, her dikey birden fazla sanal makine barındırıyorsa, hata etki alanı hiyerarşideki başka bir katmana olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-135">Conceivably, if each blade holds more than one virtual machine, there could be another layer in the Fault Domain hierarchy.</span></span>

<span data-ttu-id="7d03d-136"><center>
![Hata etki alanlarını düzenlenmiş düğümler][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="7d03d-136"><center>
![Nodes organized via Fault Domains][Image1]
</center></span></span>

<span data-ttu-id="7d03d-137">Çalışma zamanı sırasında Service Fabric kümesi Kaynak Yöneticisi hata etki alanlarını kümedeki göz önünde bulundurur ve düzenleri planları.</span><span class="sxs-lookup"><span data-stu-id="7d03d-137">During runtime, the Service Fabric Cluster Resource Manager considers the Fault Domains in the cluster and plans layouts.</span></span> <span data-ttu-id="7d03d-138">Ayrı hata etki alanı; bu nedenle durum bilgisi olan çoğaltmaları veya belirli bir hizmeti için durum bilgisiz örnek dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-138">The stateful replicas or stateless instances for a given service are distributed so they are in separate Fault Domains.</span></span> <span data-ttu-id="7d03d-139">Hata etki alanları arasında hizmet dağıtma hiyerarşinin herhangi bir düzeyde hata etki alanı başarısız olduğunda hizmetin kullanılabilirliğini tehlikeye değil sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d03d-139">Distributing the service across fault domains ensures the availability of the service is not compromised when a Fault Domain fails at any level of the hierarchy.</span></span>

<span data-ttu-id="7d03d-140">Service Fabric'ın Küme Kaynak Yöneticisi'ni kaç Katmanlar hata etki alanı hiyerarşisinde vardır önemli değil.</span><span class="sxs-lookup"><span data-stu-id="7d03d-140">Service Fabric’s Cluster Resource Manager doesn’t care how many layers there are in the Fault Domain hierarchy.</span></span> <span data-ttu-id="7d03d-141">Bununla birlikte, hiyerarşideki herhangi bir kısmının kaybı içinde çalışan hizmetler etkilemez emin olmak çalışır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-141">However, it tries to ensure that the loss of any one portion of the hierarchy doesn’t impact services running in it.</span></span> 

<span data-ttu-id="7d03d-142">Aynı sayıda her hata etki alanı hiyerarşisinde derinlik düzeyini düğüm varsa en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-142">It is best if there are the same number of nodes at each level of depth in the Fault Domain hierarchy.</span></span> <span data-ttu-id="7d03d-143">Hata etki alanı "Ağaç" kümenizdeki dengesiz ise, bu hizmetleri en iyi ayırma bulmak için Küme Kaynak Yöneticisi için zorlaştıran.</span><span class="sxs-lookup"><span data-stu-id="7d03d-143">If the “tree” of Fault Domains is unbalanced in your cluster, it makes it harder for the Cluster Resource Manager to figure out the best allocation of services.</span></span> <span data-ttu-id="7d03d-144">İmbalanced hata etki alanlarını düzenleri, bazı etki alanlarına etkisi diğer etki alanlarındaki'den fazla hizmetlerin kullanılabilirliğini kaybı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-144">Imbalanced Fault Domains layouts mean that the loss of some domains impact the availability of services more than other domains.</span></span> <span data-ttu-id="7d03d-145">Sonuç olarak, Küme Kaynak Yöneticisi'ni arasında iki amacı kaldırılır: Hizmetleri üzerlerinde koyarak "kalın" Bu etki alanında makineler kullanmak istediği ve böylece bir etki alanı kaybı sorunlara neden olmayan hizmetleri diğer etki alanlarında yerleştirmek istiyor.</span><span class="sxs-lookup"><span data-stu-id="7d03d-145">As a result, the Cluster Resource Manager is torn between two goals: It wants to use the machines in that “heavy” domain by placing services on them, and it wants to place services in other domains so that the loss of a domain doesn’t cause problems.</span></span> 

<span data-ttu-id="7d03d-146">İmbalanced etki alanları ne gibi görünüyor?</span><span class="sxs-lookup"><span data-stu-id="7d03d-146">What do imbalanced domains look like?</span></span> <span data-ttu-id="7d03d-147">Aşağıdaki diyagramda, iki farklı küme düzenleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-147">In the diagram below, we show two different cluster layouts.</span></span> <span data-ttu-id="7d03d-148">İlk örnekte düğümleri hata etki alanları arasında eşit olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-148">In the first example, the nodes are distributed evenly across the Fault Domains.</span></span> <span data-ttu-id="7d03d-149">İkinci örnekte, bir hata etki alanı, diğer bir hata etki alanları daha pek çok daha fazla düğüm yok.</span><span class="sxs-lookup"><span data-stu-id="7d03d-149">In the second example, one Fault Domain has many more nodes than the other Fault Domains.</span></span> 

<span data-ttu-id="7d03d-150"><center>
![İki farklı küme düzenleri][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="7d03d-150"><center>
![Two different cluster layouts][Image2]
</center></span></span>

<span data-ttu-id="7d03d-151">Azure üzerinde hata etki alanı bir düğümü içeren seçim sizin için yönetilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-151">In Azure, the choice of which Fault Domain contains a node is managed for you.</span></span> <span data-ttu-id="7d03d-152">Ancak, sağlamanız düğüm sayısına bağlı olarak, hala hata etki alanları ile diğerlerinden daha fazla düğüm bunlara şunun.</span><span class="sxs-lookup"><span data-stu-id="7d03d-152">However, depending on the number of nodes that you provision you can still end up with Fault Domains with more nodes in them than others.</span></span> <span data-ttu-id="7d03d-153">Örneğin, kümedeki beş hata etki alanlarını sahip ancak yedi düğümler için belirli bir NodeType sağlamasını söyleyin.</span><span class="sxs-lookup"><span data-stu-id="7d03d-153">For example, say you have five Fault Domains in the cluster but provision seven nodes for a given NodeType.</span></span> <span data-ttu-id="7d03d-154">Daha fazla düğüm ile bu durumda, ilk iki hata etki alanlarını sonlanır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-154">In this case, the first two Fault Domains end up with more nodes.</span></span> <span data-ttu-id="7d03d-155">Yalnızca birkaç örnekleri ile daha fazla NodeTypes dağıtmaya devam ederseniz, sorunu daha zayıf alır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-155">If you continue to deploy more NodeTypes with only a couple instances, the problem gets worse.</span></span> <span data-ttu-id="7d03d-156">Bu nedenle, her düğümde bulunan düğüm sayısı önerilir birden çok hata etki alanları sayısı türüdür.</span><span class="sxs-lookup"><span data-stu-id="7d03d-156">For this reason it's recommended that the number of nodes in each node type is a multiple of the number of Fault Domains.</span></span>

## <a name="upgrade-domains"></a><span data-ttu-id="7d03d-157">Yükseltme etki alanları</span><span class="sxs-lookup"><span data-stu-id="7d03d-157">Upgrade domains</span></span>
<span data-ttu-id="7d03d-158">Yükseltme etki alanları, küme düzenini anlamak Service Fabric küme Resource Manager yardımcı olan başka bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-158">Upgrade Domains are another feature that helps the Service Fabric Cluster Resource Manager understand the layout of the cluster.</span></span> <span data-ttu-id="7d03d-159">Yükseltme etki alanları aynı anda yükseltilir düğümlerinin kümelerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7d03d-159">Upgrade Domains define sets of nodes that are upgraded at the same time.</span></span> <span data-ttu-id="7d03d-160">Yükseltme etki alanlarının Küme Kaynak Yöneticisi anlamak ve yükseltme gibi yönetim işlemlerini düzenlemek yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7d03d-160">Upgrade Domains help the Cluster Resource Manager understand and orchestrate management operations like upgrades.</span></span>

<span data-ttu-id="7d03d-161">Yükseltme etki alanlarının çok hata etki alanları gibi ancak birkaç önemli farklılıklar sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-161">Upgrade Domains are a lot like Fault Domains, but with a couple key differences.</span></span> <span data-ttu-id="7d03d-162">İlk olarak, Eşgüdümlü donanım hataları alanlarının hata etki alanlarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7d03d-162">First, areas of coordinated hardware failures define Fault Domains.</span></span> <span data-ttu-id="7d03d-163">Yükseltme etki alanları, diğer yandan, ilke tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-163">Upgrade Domains, on the other hand, are defined by policy.</span></span> <span data-ttu-id="7d03d-164">Kaç tane, bu ortamı tarafından dikte yerine istediğinize karar verin alın.</span><span class="sxs-lookup"><span data-stu-id="7d03d-164">You get to decide how many you want, rather than it being dictated by the environment.</span></span> <span data-ttu-id="7d03d-165">Sayıda yükseltme düğümleri yaptığınız gibi etki alanları olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-165">You could have as many Upgrade Domains as you do nodes.</span></span> <span data-ttu-id="7d03d-166">Başka bir hata etki alanları ve yükseltme etki alanları arasında yükseltme etki alanları hiyerarşik olmayan farktır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-166">Another difference between Fault Domains and Upgrade Domains is that Upgrade Domains are not hierarchical.</span></span> <span data-ttu-id="7d03d-167">Bunun yerine, bunlar gibi basit bir etiketin daha fazla.</span><span class="sxs-lookup"><span data-stu-id="7d03d-167">Instead, they are more like a simple tag.</span></span> 

<span data-ttu-id="7d03d-168">Aşağıdaki diyagramda, üç yükseltme etki alanları üç hata etki alanlarında şeritli gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-168">The following diagram shows three Upgrade Domains are striped across three Fault Domains.</span></span> <span data-ttu-id="7d03d-169">Ayrıca, her farklı hata ve yükseltme etki alanları bittiği bir olası yerleşimini üç farklı çoğaltmalar için bir durum bilgisi olan hizmet gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-169">It also shows one possible placement for three different replicas of a stateful service, where each ends up in different Fault and Upgrade Domains.</span></span> <span data-ttu-id="7d03d-170">Bu yerleştirme hata etki alanı hizmeti yükseltmesi sırasında ortasında kaybı sağlar ve kod ve verilerin bir kopyasını çözümlenmedi.</span><span class="sxs-lookup"><span data-stu-id="7d03d-170">This placement allows the loss of a Fault Domain while in the middle of a service upgrade and still have one copy of the code and data.</span></span>  

<span data-ttu-id="7d03d-171"><center>
![Hata ve yükseltme etki alanları ile yerleştirme][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="7d03d-171"><center>
![Placement With Fault and Upgrade Domains][Image3]
</center></span></span>

<span data-ttu-id="7d03d-172">Artıları ve eksileri sahip çok sayıda yükseltme etki alanları için vardır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-172">There are pros and cons to having large numbers of Upgrade Domains.</span></span> <span data-ttu-id="7d03d-173">Daha fazla yükseltme etki alanı yükseltme her adımı daha ayrıntılı ve bu nedenle daha az sayıda düğümleri veya hizmetleri etkiler anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-173">More Upgrade Domains means each step of the upgrade is more granular and therefore affects a smaller number of nodes or services.</span></span> <span data-ttu-id="7d03d-174">Sonuç olarak, daha az Hizmetleri aynı anda taşımak daha az karmaşası sisteme giriş var.</span><span class="sxs-lookup"><span data-stu-id="7d03d-174">As a result, fewer services have to move at a time, introducing less churn into the system.</span></span> <span data-ttu-id="7d03d-175">Bu hizmetin daha az yükseltme sırasında sunulan herhangi bir sorundan etkilenmez beri güvenilirliğini, artırmak eğilimindedir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-175">This tends to improve reliability, since less of the service is impacted by any issue introduced during the upgrade.</span></span> <span data-ttu-id="7d03d-176">Daha fazla yükseltme etki alanları ayrıca diğer düğümlerdeki yükseltme etkisini işlemek için daha az arabellek gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-176">More Upgrade Domains also means that you need less available buffer on other nodes to handle the impact of the upgrade.</span></span> <span data-ttu-id="7d03d-177">Örneğin, beş yükseltme etki alanları varsa, her düğüm trafiğinizi % 20 işleme kabaca.</span><span class="sxs-lookup"><span data-stu-id="7d03d-177">For example, if you have five Upgrade Domains, the nodes in each are handling roughly 20% of your traffic.</span></span> <span data-ttu-id="7d03d-178">Bu yükseltme etki alanı için bir yükseltme aşağı olması gerekiyorsa, bu Yük genellikle bir yere gitmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-178">If you need to take down that Upgrade Domain for an upgrade, that load usually needs to go somewhere.</span></span> <span data-ttu-id="7d03d-179">Dört kalan yükseltme etki alanları sahip olduğundan, her yaklaşık %5 toplam trafik için yeriniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-179">Since you have four remaining Upgrade Domains, each must have room for about 5% of the total traffic.</span></span> <span data-ttu-id="7d03d-180">Daha fazla yükseltme etki alanları kümedeki düğümler üzerinde daha az arabellek ihtiyaç duyacağınız anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-180">More Upgrade Domains means you need less buffer on the nodes in the cluster.</span></span> <span data-ttu-id="7d03d-181">Örneğin, 10 yükseltme etki alanları yerine sahip olmadığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="7d03d-181">For example, consider if you had 10 Upgrade Domains instead.</span></span> <span data-ttu-id="7d03d-182">Bu durumda, her UD yalnızca yaklaşık %10 toplam trafik işleme.</span><span class="sxs-lookup"><span data-stu-id="7d03d-182">In that case, each UD would only be handling about 10% of the total traffic.</span></span> <span data-ttu-id="7d03d-183">Bir yükseltme adımları, küme aracılığıyla her etki alanı yalnızca yaklaşık %1.1 toplam trafik için yeriniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-183">When an upgrade steps through the cluster, each domain would only need to have room for about 1.1% of the total traffic.</span></span> <span data-ttu-id="7d03d-184">Daha fazla yükseltme etki alanları genellikle, daha az ayrılmış kapasite gerektiğinden düğümleriniz yüksek kullanımı, çalıştırmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d03d-184">More Upgrade Domains generally allow you to run your nodes at higher utilization, since you need less reserved capacity.</span></span> <span data-ttu-id="7d03d-185">Aynı hata etki alanları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-185">The same is true for Fault Domains.</span></span>  

<span data-ttu-id="7d03d-186">Birden çok etki alanı yükseltme sonucunda dezavantajı, yükseltmeler daha uzun sürer eğilimindedir ' dir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-186">The downside of having many Upgrade Domains is that upgrades tend to take longer.</span></span> <span data-ttu-id="7d03d-187">Service Fabric yükseltme etki alanı tamamlandıktan ve bir sonraki yükseltmeye başlamadan önce bir denetim gerçekleştirmediğini saat kısa bir süre bekler.</span><span class="sxs-lookup"><span data-stu-id="7d03d-187">Service Fabric waits a short period of time after an Upgrade Domain is completed and performs checks before starting to upgrade the next one.</span></span> <span data-ttu-id="7d03d-188">Bu gecikmeler yükseltmeye devam etmeden önce yükseltme tarafından sunulan algılama sorunları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7d03d-188">These delays enable detecting issues introduced by the upgrade before the upgrade proceeds.</span></span> <span data-ttu-id="7d03d-189">Kolaylığını kabul edilebilir olduğundan aynı anda hizmeti çok fazla etkilemesini hatalı değişiklikleri önler.</span><span class="sxs-lookup"><span data-stu-id="7d03d-189">The tradeoff is acceptable because it prevents bad changes from affecting too much of the service at a time.</span></span>

<span data-ttu-id="7d03d-190">Çok az yükseltme etki alanına sahip birçok negatif yan etkileri – tek tek her yükseltme etki alanı aşağı ve büyük bölümünü yükseltiliyor genel kapasitenizi kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="7d03d-190">Too few Upgrade Domains has many negative side effects – while each individual Upgrade Domain is down and being upgraded a large portion of your overall capacity is unavailable.</span></span> <span data-ttu-id="7d03d-191">Örneğin, yalnızca üç yükseltme etki alanı varsa, aynı anda yaklaşık 1/3 genel hizmet veya küme kapasite sürüyor.</span><span class="sxs-lookup"><span data-stu-id="7d03d-191">For example, if you only have three Upgrade Domains you are taking down about 1/3 of your overall service or cluster capacity at a time.</span></span> <span data-ttu-id="7d03d-192">İş yükünü işlemek için kümenizi geri kalanı yeterli kapasiteye sahip olmanız bu yana çok hizmetinizin aşağı aynı anda sahip arzu değil.</span><span class="sxs-lookup"><span data-stu-id="7d03d-192">Having so much of your service down at once isn’t desirable since you have to have enough capacity in the rest of your cluster to handle the workload.</span></span> <span data-ttu-id="7d03d-193">Bu arabellek anlamına gelir normal işlemi sırasında aksi durumdakinden daha az yüklenen düğümleri olan koruma.</span><span class="sxs-lookup"><span data-stu-id="7d03d-193">Maintaining that buffer means that during normal operation those nodes are less loaded than they would be otherwise.</span></span> <span data-ttu-id="7d03d-194">Bu, hizmetiniz çalıştırma maliyetini artırır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-194">This increases the cost of running your service.</span></span>

<span data-ttu-id="7d03d-195">Toplam sayısına hatası veya yükseltme etki alanlarının bir ortam ya da nasıl birbiriyle kısıtlamaları gerçek bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="7d03d-195">There’s no real limit to the total number of fault or Upgrade Domains in an environment, or constraints on how they overlap.</span></span> <span data-ttu-id="7d03d-196">Birkaç ortak desenler vardır Bununla:</span><span class="sxs-lookup"><span data-stu-id="7d03d-196">That said, there are several common patterns:</span></span>

- <span data-ttu-id="7d03d-197">Hata etki alanları ve yükseltme etki alanları 1:1 eşlenmiş</span><span class="sxs-lookup"><span data-stu-id="7d03d-197">Fault Domains and Upgrade Domains mapped 1:1</span></span>
- <span data-ttu-id="7d03d-198">Bir yükseltme etki alanı her düğüm (fiziksel veya sanal işletim sistemi örneği)</span><span class="sxs-lookup"><span data-stu-id="7d03d-198">One Upgrade Domain per Node (physical or virtual OS instance)</span></span>
- <span data-ttu-id="7d03d-199">Burada hata etki alanları ve yükseltme etki alanı bir matris genellikle çizgileri çalışan makineler ile form "şeritli" veya "matris" modeli</span><span class="sxs-lookup"><span data-stu-id="7d03d-199">A “striped” or “matrix” model where the Fault Domains and Upgrade Domains form a matrix with machines usually running down the diagonals</span></span>

<span data-ttu-id="7d03d-200"><center>
![Hata ve yükseltme etki alanı düzenleri][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="7d03d-200"><center>
![Fault and Upgrade Domain Layouts][Image4]
</center></span></span>

<span data-ttu-id="7d03d-201">Hangi düzenin seçmek için hiçbir en iyi yanıt, her bazı Artıları ve eksileri vardır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-201">There’s no best answer which layout to choose, each has some pros and cons.</span></span> <span data-ttu-id="7d03d-202">Örneğin, 1FD:1UD modeli ayarlamak basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-202">For example, the 1FD:1UD model is simple to set up.</span></span> <span data-ttu-id="7d03d-203">1 yükseltme etki alanı düğümü modeli başına hangi kişiler için kullanılan gibi çoğu'dir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-203">The 1 Upgrade Domain per Node model is most like what people are used to.</span></span> <span data-ttu-id="7d03d-204">Yükseltme sırasında her düğüm bağımsız olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-204">During upgrades each node is updated independently.</span></span> <span data-ttu-id="7d03d-205">Bu, nasıl küçük makineler kümesini el ile geçmişte yükseltilen için benzer.</span><span class="sxs-lookup"><span data-stu-id="7d03d-205">This is similar to how small sets of machines were upgraded manually in the past.</span></span> 

<span data-ttu-id="7d03d-206">Burada FDs ve UDs bir tablo oluşturur ve düğümler çapraz başlangıç yerleştirilir FD/UD matris en yaygın modelidir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-206">The most common model is the FD/UD matrix, where the FDs and UDs form a table and nodes are placed starting along the diagonal.</span></span> <span data-ttu-id="7d03d-207">Bu, varsayılan olarak Azure Service Fabric kümelerinde kullanılan modelidir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-207">This is the model used by default in Service Fabric clusters in Azure.</span></span> <span data-ttu-id="7d03d-208">Birçok düğümleri içeren kümeler için her şeyi yukarıdaki yoğun matris düzeni gibi bakan sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-208">For clusters with many nodes everything ends up looking like the dense matrix pattern above.</span></span>

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a><span data-ttu-id="7d03d-209">Hata ve yükseltme etki alanı kısıtlamaları ve bunun sonucunda oluşan davranışı</span><span class="sxs-lookup"><span data-stu-id="7d03d-209">Fault and Upgrade Domain constraints and resulting behavior</span></span>
<span data-ttu-id="7d03d-210">Küme Kaynak Yöneticisi'ni tutmak arıza ve kısıtlama olarak yükseltme etki alanları arasında dengeli bir hizmet isteğini işler.</span><span class="sxs-lookup"><span data-stu-id="7d03d-210">The Cluster Resource Manager treats the desire to keep a service balanced across fault and Upgrade Domains as a constraint.</span></span> <span data-ttu-id="7d03d-211">Kısıtlamalar hakkında daha fazla bilgi için [bu makalede](service-fabric-cluster-resource-manager-management-integration.md).</span><span class="sxs-lookup"><span data-stu-id="7d03d-211">You can find out more about constraints in [this article](service-fabric-cluster-resource-manager-management-integration.md).</span></span> <span data-ttu-id="7d03d-212">Hata ve yükseltme etki alanı kısıtlamaları durumu: "verili hizmet bölüm için hiçbir zaman olması gerektiğini fark *birden büyük* arasında hizmet nesneleri (durum bilgisiz hizmet örneği veya durum bilgisi olan hizmet çoğaltmaları) sayısı iki etki alanı."</span><span class="sxs-lookup"><span data-stu-id="7d03d-212">The Fault and Upgrade Domain constraints state: "For a given service partition there should never be a difference *greater than one* in the number of service objects (stateless service instances or stateful service replicas) between two domains."</span></span> <span data-ttu-id="7d03d-213">Bu, belirli taşır veya bu kısıtlamayı ihlal hazırlıklara önler.</span><span class="sxs-lookup"><span data-stu-id="7d03d-213">This prevents certain moves or arrangements that violate this constraint.</span></span>

<span data-ttu-id="7d03d-214">Bir örneğe bakalım.</span><span class="sxs-lookup"><span data-stu-id="7d03d-214">Let's look at one example.</span></span> <span data-ttu-id="7d03d-215">Altı düğümü, beş hata etki alanları ve beş yükseltme etki alanları ile yapılandırılmış bir kümeye sahip olduğunuzu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="7d03d-215">Let's say that we have a cluster with six nodes, configured with five Fault Domains and five Upgrade Domains.</span></span>

|  | <span data-ttu-id="7d03d-216">FD0</span><span class="sxs-lookup"><span data-stu-id="7d03d-216">FD0</span></span> | <span data-ttu-id="7d03d-217">FD1</span><span class="sxs-lookup"><span data-stu-id="7d03d-217">FD1</span></span> | <span data-ttu-id="7d03d-218">FD2</span><span class="sxs-lookup"><span data-stu-id="7d03d-218">FD2</span></span> | <span data-ttu-id="7d03d-219">FD3</span><span class="sxs-lookup"><span data-stu-id="7d03d-219">FD3</span></span> | <span data-ttu-id="7d03d-220">FD4</span><span class="sxs-lookup"><span data-stu-id="7d03d-220">FD4</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="7d03d-221">**UD0**</span><span class="sxs-lookup"><span data-stu-id="7d03d-221">**UD0**</span></span> |<span data-ttu-id="7d03d-222">N1</span><span class="sxs-lookup"><span data-stu-id="7d03d-222">N1</span></span> | | | | |
| <span data-ttu-id="7d03d-223">**UD1**</span><span class="sxs-lookup"><span data-stu-id="7d03d-223">**UD1**</span></span> |<span data-ttu-id="7d03d-224">N6</span><span class="sxs-lookup"><span data-stu-id="7d03d-224">N6</span></span> |<span data-ttu-id="7d03d-225">N2</span><span class="sxs-lookup"><span data-stu-id="7d03d-225">N2</span></span> | | | |
| <span data-ttu-id="7d03d-226">**UD2**</span><span class="sxs-lookup"><span data-stu-id="7d03d-226">**UD2**</span></span> | | |<span data-ttu-id="7d03d-227">N3</span><span class="sxs-lookup"><span data-stu-id="7d03d-227">N3</span></span> | | |
| <span data-ttu-id="7d03d-228">**UD3**</span><span class="sxs-lookup"><span data-stu-id="7d03d-228">**UD3**</span></span> | | | |<span data-ttu-id="7d03d-229">N4</span><span class="sxs-lookup"><span data-stu-id="7d03d-229">N4</span></span> | |
| <span data-ttu-id="7d03d-230">**UD4**</span><span class="sxs-lookup"><span data-stu-id="7d03d-230">**UD4**</span></span> | | | | |<span data-ttu-id="7d03d-231">N5</span><span class="sxs-lookup"><span data-stu-id="7d03d-231">N5</span></span> |

<span data-ttu-id="7d03d-232">Şimdi biz bir TargetReplicaSetSize ile (veya Instancecount bir durum bilgisi olmayan bir hizmet için) bir hizmet beş oluşturduğunuzu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="7d03d-232">Now let's say that we create a service with a TargetReplicaSetSize (or, for a stateless service an InstanceCount) of five.</span></span> <span data-ttu-id="7d03d-233">Çoğaltmaları kara N1 N5 üzerinde.</span><span class="sxs-lookup"><span data-stu-id="7d03d-233">The replicas land on N1-N5.</span></span> <span data-ttu-id="7d03d-234">Aslında, N6 hiçbir zaman kaç Hizmetleri bu oluşturduğunuz gibi olsun kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-234">In fact, N6 is never used no matter how many services like this you create.</span></span> <span data-ttu-id="7d03d-235">Ancak neden?</span><span class="sxs-lookup"><span data-stu-id="7d03d-235">But why?</span></span> <span data-ttu-id="7d03d-236">Geçerli düzen ve N6 seçilirse ne olacağını arasındaki farkı bakalım.</span><span class="sxs-lookup"><span data-stu-id="7d03d-236">Let's look at the difference between the current layout and what would happen if N6 is chosen.</span></span>

<span data-ttu-id="7d03d-237">İşte, biz var düzeni ve çoğaltmaları hata ve yükseltme etki alanı başına toplam sayısı:</span><span class="sxs-lookup"><span data-stu-id="7d03d-237">Here's the layout we got and the total number of replicas per Fault and Upgrade Domain:</span></span>

|  | <span data-ttu-id="7d03d-238">FD0</span><span class="sxs-lookup"><span data-stu-id="7d03d-238">FD0</span></span> | <span data-ttu-id="7d03d-239">FD1</span><span class="sxs-lookup"><span data-stu-id="7d03d-239">FD1</span></span> | <span data-ttu-id="7d03d-240">FD2</span><span class="sxs-lookup"><span data-stu-id="7d03d-240">FD2</span></span> | <span data-ttu-id="7d03d-241">FD3</span><span class="sxs-lookup"><span data-stu-id="7d03d-241">FD3</span></span> | <span data-ttu-id="7d03d-242">FD4</span><span class="sxs-lookup"><span data-stu-id="7d03d-242">FD4</span></span> | <span data-ttu-id="7d03d-243">UDTotal</span><span class="sxs-lookup"><span data-stu-id="7d03d-243">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="7d03d-244">**UD0**</span><span class="sxs-lookup"><span data-stu-id="7d03d-244">**UD0**</span></span> |<span data-ttu-id="7d03d-245">R1</span><span class="sxs-lookup"><span data-stu-id="7d03d-245">R1</span></span> | | | | |<span data-ttu-id="7d03d-246">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-246">1</span></span> |
| <span data-ttu-id="7d03d-247">**UD1**</span><span class="sxs-lookup"><span data-stu-id="7d03d-247">**UD1**</span></span> | |<span data-ttu-id="7d03d-248">R2</span><span class="sxs-lookup"><span data-stu-id="7d03d-248">R2</span></span> | | | |<span data-ttu-id="7d03d-249">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-249">1</span></span> |
| <span data-ttu-id="7d03d-250">**UD2**</span><span class="sxs-lookup"><span data-stu-id="7d03d-250">**UD2**</span></span> | | |<span data-ttu-id="7d03d-251">R3</span><span class="sxs-lookup"><span data-stu-id="7d03d-251">R3</span></span> | | |<span data-ttu-id="7d03d-252">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-252">1</span></span> |
| <span data-ttu-id="7d03d-253">**UD3**</span><span class="sxs-lookup"><span data-stu-id="7d03d-253">**UD3**</span></span> | | | |<span data-ttu-id="7d03d-254">R4</span><span class="sxs-lookup"><span data-stu-id="7d03d-254">R4</span></span> | |<span data-ttu-id="7d03d-255">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-255">1</span></span> |
| <span data-ttu-id="7d03d-256">**UD4**</span><span class="sxs-lookup"><span data-stu-id="7d03d-256">**UD4**</span></span> | | | | |<span data-ttu-id="7d03d-257">R5</span><span class="sxs-lookup"><span data-stu-id="7d03d-257">R5</span></span> |<span data-ttu-id="7d03d-258">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-258">1</span></span> |
| <span data-ttu-id="7d03d-259">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="7d03d-259">**FDTotal**</span></span> |<span data-ttu-id="7d03d-260">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-260">1</span></span> |<span data-ttu-id="7d03d-261">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-261">1</span></span> |<span data-ttu-id="7d03d-262">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-262">1</span></span> |<span data-ttu-id="7d03d-263">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-263">1</span></span> |<span data-ttu-id="7d03d-264">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-264">1</span></span> |- |

<span data-ttu-id="7d03d-265">Bu düzen, hata etki alanı ve yükseltme etki alanı başına düğüm bakımından dengelenir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-265">This layout is balanced in terms of nodes per Fault Domain and Upgrade Domain.</span></span> <span data-ttu-id="7d03d-266">Ayrıca, hata ve yükseltme etki alanı başına çoğaltmaların sayısı bakımından dengelenir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-266">It is also balanced in terms of the number of replicas per Fault and Upgrade Domain.</span></span> <span data-ttu-id="7d03d-267">Her etki alanı düğümleri aynı sayıda ve çoğaltmaları aynı sayıda sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-267">Each domain has the same number of nodes and the same number of replicas.</span></span>

<span data-ttu-id="7d03d-268">Şimdi, N6 yerine N2 kullandık neler olacağını konumundaki bakalım.</span><span class="sxs-lookup"><span data-stu-id="7d03d-268">Now, let's look at what would happen if we'd used N6 instead of N2.</span></span> <span data-ttu-id="7d03d-269">Nasıl çoğaltmaları sonra dağıtılmış?</span><span class="sxs-lookup"><span data-stu-id="7d03d-269">How would the replicas be distributed then?</span></span>

|  | <span data-ttu-id="7d03d-270">FD0</span><span class="sxs-lookup"><span data-stu-id="7d03d-270">FD0</span></span> | <span data-ttu-id="7d03d-271">FD1</span><span class="sxs-lookup"><span data-stu-id="7d03d-271">FD1</span></span> | <span data-ttu-id="7d03d-272">FD2</span><span class="sxs-lookup"><span data-stu-id="7d03d-272">FD2</span></span> | <span data-ttu-id="7d03d-273">FD3</span><span class="sxs-lookup"><span data-stu-id="7d03d-273">FD3</span></span> | <span data-ttu-id="7d03d-274">FD4</span><span class="sxs-lookup"><span data-stu-id="7d03d-274">FD4</span></span> | <span data-ttu-id="7d03d-275">UDTotal</span><span class="sxs-lookup"><span data-stu-id="7d03d-275">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="7d03d-276">**UD0**</span><span class="sxs-lookup"><span data-stu-id="7d03d-276">**UD0**</span></span> |<span data-ttu-id="7d03d-277">R1</span><span class="sxs-lookup"><span data-stu-id="7d03d-277">R1</span></span> | | | | |<span data-ttu-id="7d03d-278">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-278">1</span></span> |
| <span data-ttu-id="7d03d-279">**UD1**</span><span class="sxs-lookup"><span data-stu-id="7d03d-279">**UD1**</span></span> |<span data-ttu-id="7d03d-280">R5</span><span class="sxs-lookup"><span data-stu-id="7d03d-280">R5</span></span> | | | | |<span data-ttu-id="7d03d-281">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-281">1</span></span> |
| <span data-ttu-id="7d03d-282">**UD2**</span><span class="sxs-lookup"><span data-stu-id="7d03d-282">**UD2**</span></span> | | |<span data-ttu-id="7d03d-283">R2</span><span class="sxs-lookup"><span data-stu-id="7d03d-283">R2</span></span> | | |<span data-ttu-id="7d03d-284">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-284">1</span></span> |
| <span data-ttu-id="7d03d-285">**UD3**</span><span class="sxs-lookup"><span data-stu-id="7d03d-285">**UD3**</span></span> | | | |<span data-ttu-id="7d03d-286">R3</span><span class="sxs-lookup"><span data-stu-id="7d03d-286">R3</span></span> | |<span data-ttu-id="7d03d-287">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-287">1</span></span> |
| <span data-ttu-id="7d03d-288">**UD4**</span><span class="sxs-lookup"><span data-stu-id="7d03d-288">**UD4**</span></span> | | | | |<span data-ttu-id="7d03d-289">R4</span><span class="sxs-lookup"><span data-stu-id="7d03d-289">R4</span></span> |<span data-ttu-id="7d03d-290">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-290">1</span></span> |
| <span data-ttu-id="7d03d-291">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="7d03d-291">**FDTotal**</span></span> |<span data-ttu-id="7d03d-292">2</span><span class="sxs-lookup"><span data-stu-id="7d03d-292">2</span></span> |<span data-ttu-id="7d03d-293">0</span><span class="sxs-lookup"><span data-stu-id="7d03d-293">0</span></span> |<span data-ttu-id="7d03d-294">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-294">1</span></span> |<span data-ttu-id="7d03d-295">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-295">1</span></span> |<span data-ttu-id="7d03d-296">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-296">1</span></span> |- |

<span data-ttu-id="7d03d-297">Bu düzen, hata etki alanı kısıtlaması için bizim tanımını ihlal ediyor.</span><span class="sxs-lookup"><span data-stu-id="7d03d-297">This layout violates our definition for the Fault Domain constraint.</span></span> <span data-ttu-id="7d03d-298">FD1 iki toplam FD0 FD1 arasındaki fark yapmadan sıfır sahipken FD0 iki çoğaltması yok.</span><span class="sxs-lookup"><span data-stu-id="7d03d-298">FD0 has two replicas, while FD1 has zero, making the difference between FD0 and FD1 a total of two.</span></span> <span data-ttu-id="7d03d-299">Küme Kaynak Yöneticisi, bu düzenleme izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="7d03d-299">The Cluster Resource Manager does not allow this arrangement.</span></span> <span data-ttu-id="7d03d-300">Benzer şekilde biz N2 ve N6 (yerine N1 ve N2) kaldırdıysa biz alın:</span><span class="sxs-lookup"><span data-stu-id="7d03d-300">Similarly if we picked N2 and N6 (instead of N1 and N2) we'd get:</span></span>

|  | <span data-ttu-id="7d03d-301">FD0</span><span class="sxs-lookup"><span data-stu-id="7d03d-301">FD0</span></span> | <span data-ttu-id="7d03d-302">FD1</span><span class="sxs-lookup"><span data-stu-id="7d03d-302">FD1</span></span> | <span data-ttu-id="7d03d-303">FD2</span><span class="sxs-lookup"><span data-stu-id="7d03d-303">FD2</span></span> | <span data-ttu-id="7d03d-304">FD3</span><span class="sxs-lookup"><span data-stu-id="7d03d-304">FD3</span></span> | <span data-ttu-id="7d03d-305">FD4</span><span class="sxs-lookup"><span data-stu-id="7d03d-305">FD4</span></span> | <span data-ttu-id="7d03d-306">UDTotal</span><span class="sxs-lookup"><span data-stu-id="7d03d-306">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="7d03d-307">**UD0**</span><span class="sxs-lookup"><span data-stu-id="7d03d-307">**UD0**</span></span> | | | | | |<span data-ttu-id="7d03d-308">0</span><span class="sxs-lookup"><span data-stu-id="7d03d-308">0</span></span> |
| <span data-ttu-id="7d03d-309">**UD1**</span><span class="sxs-lookup"><span data-stu-id="7d03d-309">**UD1**</span></span> |<span data-ttu-id="7d03d-310">R5</span><span class="sxs-lookup"><span data-stu-id="7d03d-310">R5</span></span> |<span data-ttu-id="7d03d-311">R1</span><span class="sxs-lookup"><span data-stu-id="7d03d-311">R1</span></span> | | | |<span data-ttu-id="7d03d-312">2</span><span class="sxs-lookup"><span data-stu-id="7d03d-312">2</span></span> |
| <span data-ttu-id="7d03d-313">**UD2**</span><span class="sxs-lookup"><span data-stu-id="7d03d-313">**UD2**</span></span> | | |<span data-ttu-id="7d03d-314">R2</span><span class="sxs-lookup"><span data-stu-id="7d03d-314">R2</span></span> | | |<span data-ttu-id="7d03d-315">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-315">1</span></span> |
| <span data-ttu-id="7d03d-316">**UD3**</span><span class="sxs-lookup"><span data-stu-id="7d03d-316">**UD3**</span></span> | | | |<span data-ttu-id="7d03d-317">R3</span><span class="sxs-lookup"><span data-stu-id="7d03d-317">R3</span></span> | |<span data-ttu-id="7d03d-318">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-318">1</span></span> |
| <span data-ttu-id="7d03d-319">**UD4**</span><span class="sxs-lookup"><span data-stu-id="7d03d-319">**UD4**</span></span> | | | | |<span data-ttu-id="7d03d-320">R4</span><span class="sxs-lookup"><span data-stu-id="7d03d-320">R4</span></span> |<span data-ttu-id="7d03d-321">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-321">1</span></span> |
| <span data-ttu-id="7d03d-322">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="7d03d-322">**FDTotal**</span></span> |<span data-ttu-id="7d03d-323">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-323">1</span></span> |<span data-ttu-id="7d03d-324">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-324">1</span></span> |<span data-ttu-id="7d03d-325">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-325">1</span></span> |<span data-ttu-id="7d03d-326">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-326">1</span></span> |<span data-ttu-id="7d03d-327">1</span><span class="sxs-lookup"><span data-stu-id="7d03d-327">1</span></span> |- |

<span data-ttu-id="7d03d-328">Bu düzen, hata etki alanlarını bakımından dengelenir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-328">This layout is balanced in terms of Fault Domains.</span></span> <span data-ttu-id="7d03d-329">Bununla birlikte, artık bu etki alanı yükseltme kısıtlaması ihlal.</span><span class="sxs-lookup"><span data-stu-id="7d03d-329">However, now it's violating the Upgrade Domain constraint.</span></span> <span data-ttu-id="7d03d-330">UD1 iki sahipken UD0 sıfır çoğaltmalarına sahip olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-330">This is because UD0 has zero replicas while UD1 has two.</span></span> <span data-ttu-id="7d03d-331">Bu nedenle, bu düzeni ayrıca geçersiz ve küme kaynak yönetici tarafından çekilmesi olmaz.</span><span class="sxs-lookup"><span data-stu-id="7d03d-331">Therefore, this layout is also invalid and won't be picked by the Cluster Resource Manager.</span></span> 

## <a name="configuring-fault-and-upgrade-domains"></a><span data-ttu-id="7d03d-332">Hata ve yükseltme etki alanlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7d03d-332">Configuring fault and Upgrade Domains</span></span>
<span data-ttu-id="7d03d-333">Hata etki alanları ve yükseltme etki alanları tanımlama yapılır otomatik olarak Azure Service Fabric dağıtımları barındırılan.</span><span class="sxs-lookup"><span data-stu-id="7d03d-333">Defining Fault Domains and Upgrade Domains is done automatically in Azure hosted Service Fabric deployments.</span></span> <span data-ttu-id="7d03d-334">Service Fabric alır ve Azure ortamı bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-334">Service Fabric picks up and uses the environment information from Azure.</span></span>

<span data-ttu-id="7d03d-335">Kendi kümenizi oluşturmakta olduğunuz (veya belirli bir topolojisi geliştirme çalıştırmak istediğiniz varsa), hata etki alanı ve etki alanı yükseltme bilgileri kendiniz sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-335">If you’re creating your own cluster (or want to run a particular topology in development), you can provide the Fault Domain and Upgrade Domain information yourself.</span></span> <span data-ttu-id="7d03d-336">Bu örnekte, üç "veri merkezleri" (her üç rafları) yayılan dokuz düğümlü bir yerel geliştirme küme tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7d03d-336">In this example, we define a nine node local development cluster that spans three “datacenters” (each with three racks).</span></span> <span data-ttu-id="7d03d-337">Bu küme üç yükseltme bu üç veri merkezi arasında şeritli etki alanı da sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-337">This cluster also has three Upgrade Domains striped across those three datacenters.</span></span> <span data-ttu-id="7d03d-338">Yapılandırma örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="7d03d-338">An example of the configuration is below:</span></span> 

<span data-ttu-id="7d03d-339">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="7d03d-339">ClusterManifest.xml</span></span>

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

<span data-ttu-id="7d03d-340">tek başına dağıtımlarında ClusterConfig.json</span><span class="sxs-lookup"><span data-stu-id="7d03d-340">via ClusterConfig.json for Standalone deployments</span></span>

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> <span data-ttu-id="7d03d-341">Kümeler Azure Resource Manager aracılığıyla tanımlarken, hata etki alanları ve yükseltme etki alanlarının Azure tarafından atanır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-341">When defining clusters via Azure Resource Manager, Fault Domains and Upgrade Domains are assigned by Azure.</span></span> <span data-ttu-id="7d03d-342">Bu nedenle, Azure Resource Manager şablonu düğüm türleri ve sanal makine ölçek kümeleri tanımında hata etki alanı veya etki alanı yükseltme bilgileri içermez.</span><span class="sxs-lookup"><span data-stu-id="7d03d-342">Therefore, the definition of your Node Types and Virtual Machine Scale Sets in your Azure Resource Manager template does not include Fault Domain or Upgrade Domain information.</span></span>
>

## <a name="node-properties-and-placement-constraints"></a><span data-ttu-id="7d03d-343">Düğüm özellikleri ve yerleştirme kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="7d03d-343">Node properties and placement constraints</span></span>
<span data-ttu-id="7d03d-344">Bazen (aslında, çoğu zaman), belirli iş yükleri yalnızca belirli türde bir kümedeki düğümler üzerinde çalıştığından emin olmak istediğiniz oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="7d03d-344">Sometimes (in fact, most of the time) you’re going to want to ensure that certain workloads run only on certain types of nodes in the cluster.</span></span> <span data-ttu-id="7d03d-345">Örneğin, diğerleri olmayabilir ancak bazı iş yükü GPU veya SSD gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-345">For example, some workload may require GPUs or SSDs while others may not.</span></span> <span data-ttu-id="7d03d-346">Neredeyse her n katmanlı mimarisi ölçeklendiriyor belirli iş yükleri için donanım hedefleme harika bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-346">A great example of targeting hardware to particular workloads is almost every n-tier architecture out there.</span></span> <span data-ttu-id="7d03d-347">Belirli makineler ön uç veya uygulamanın tarafı hizmet veren API hizmet ve istemcilerin veya Internet'e gösteriliyor.</span><span class="sxs-lookup"><span data-stu-id="7d03d-347">Certain machines serve as the front end or API serving side of the application and are exposed to the clients or the internet.</span></span> <span data-ttu-id="7d03d-348">Genellikle, farklı donanım kaynakları olan farklı makinelerde işlem ya da depolama katmanları iş işleyin.</span><span class="sxs-lookup"><span data-stu-id="7d03d-348">Different machines, often with different hardware resources, handle the work of the compute or storage layers.</span></span> <span data-ttu-id="7d03d-349">Çoğunlukla bunlar _değil_ doğrudan istemcileri veya Internet'e açık.</span><span class="sxs-lookup"><span data-stu-id="7d03d-349">These are usually _not_ directly exposed to clients or the internet.</span></span> <span data-ttu-id="7d03d-350">Service Fabric burada belirli donanım yapılandırmalarını temel çalıştırmak için belirli iş yükleri gereken durumlar vardır bekliyor.</span><span class="sxs-lookup"><span data-stu-id="7d03d-350">Service Fabric expects that there are cases where particular workloads need to run on particular hardware configurations.</span></span> <span data-ttu-id="7d03d-351">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7d03d-351">For example:</span></span>

* <span data-ttu-id="7d03d-352">bir Service Fabric ortamına varolan n katmanlı uygulama "kaldırılmış ve gölgeye" olarak adlandırılmıştır</span><span class="sxs-lookup"><span data-stu-id="7d03d-352">an existing n-tier application has been “lifted and shifted” into a Service Fabric environment</span></span>
* <span data-ttu-id="7d03d-353">bir iş yükü performansı, ölçek ve güvenlik yalıtımı nedeniyle belirli donanım üzerinde çalıştırmak istiyor</span><span class="sxs-lookup"><span data-stu-id="7d03d-353">a workload wants to run on specific hardware for performance, scale, or security isolation reasons</span></span>
* <span data-ttu-id="7d03d-354">Bir iş yükü İlkesi ya da kaynak tüketimi nedeniyle diğer iş yüklerini üzerinden olmalıdır</span><span class="sxs-lookup"><span data-stu-id="7d03d-354">A workload should be isolated from other workloads for policy or resource consumption reasons</span></span>

<span data-ttu-id="7d03d-355">Bu tür yapılandırmaları desteklemek için Service Fabric düğümlere uygulanan etiketleri birinci sınıf kavramı vardır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-355">To support these sorts of configurations, Service Fabric has a first class notion of tags that can be applied to nodes.</span></span> <span data-ttu-id="7d03d-356">Bu etiketler adlı **düğümü özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="7d03d-356">These tags are called **node properties**.</span></span> <span data-ttu-id="7d03d-357">**Kısıtlamalarından** olan bir veya daha fazla düğüm özelliklerini seçin, tek tek hizmetlerine bağlı deyimleri.</span><span class="sxs-lookup"><span data-stu-id="7d03d-357">**Placement constraints** are the statements attached to individual services that select for one or more node properties.</span></span> <span data-ttu-id="7d03d-358">Kısıtlamalarından Hizmetleri çalıştırdığı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7d03d-358">Placement constraints define where services should run.</span></span> <span data-ttu-id="7d03d-359">Kısıtlamalar kümesini Genişletilebilir - herhangi bir anahtar/değer çifti çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d03d-359">The set of constraints is extensible - any key/value pair can work.</span></span> 

<span data-ttu-id="7d03d-360"><center>
![Düzen farklı iş yükleri küme][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="7d03d-360"><center>
![Cluster Layout Different Workloads][Image5]
</center></span></span>

### <a name="built-in-node-properties"></a><span data-ttu-id="7d03d-361">Düğüm özellikleri yerleşik</span><span class="sxs-lookup"><span data-stu-id="7d03d-361">Built in node properties</span></span>
<span data-ttu-id="7d03d-362">Service Fabric kullanıcının tanımlamadan gerek kalmadan otomatik olarak kullanılabilecek bazı varsayılan düğüm özelliklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7d03d-362">Service Fabric defines some default node properties that can be used automatically without the user having to define them.</span></span> <span data-ttu-id="7d03d-363">Her düğümde tanımlanan varsayılan Özellikler **NodeType** ve **NodeName**.</span><span class="sxs-lookup"><span data-stu-id="7d03d-363">The default properties defined at each node are the **NodeType** and the **NodeName**.</span></span> <span data-ttu-id="7d03d-364">Bu nedenle örneğin yerleştirme kısıtlama olarak yazabilirsiniz `"(NodeType == NodeType03)"`.</span><span class="sxs-lookup"><span data-stu-id="7d03d-364">So for example you could write a placement constraint as `"(NodeType == NodeType03)"`.</span></span> <span data-ttu-id="7d03d-365">Genellikle en yaygın olarak uygulanacak NodeType özelliklerinin kullanılmasını buldunuz.</span><span class="sxs-lookup"><span data-stu-id="7d03d-365">Generally we have found NodeType to be one of the most commonly used properties.</span></span> <span data-ttu-id="7d03d-366">Bir makine türüyle 1:1 karşılık gelen beri yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="7d03d-366">It is useful since it corresponds 1:1 with a type of a machine.</span></span> <span data-ttu-id="7d03d-367">Her makine türü geleneksel n katmanlı uygulama iş yükü türünü karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-367">Each type of machine corresponds to a type of workload in a traditional n-tier application.</span></span>

<span data-ttu-id="7d03d-368"><center>
![Yerleştirme kısıtlamaları ve düğüm özellikleri][Image6]
</center></span><span class="sxs-lookup"><span data-stu-id="7d03d-368"><center>
![Placement Constraints and Node Properties][Image6]
</center></span></span>

## <a name="placement-constraint-and-node-property-syntax"></a><span data-ttu-id="7d03d-369">Yerleştirme kısıtlaması ve düğüm özellik sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7d03d-369">Placement Constraint and Node Property Syntax</span></span> 
<span data-ttu-id="7d03d-370">Düğüm özelliğinde belirtilen değeri veya uzun imzalı bir string, bool, olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-370">The value specified in the node property can be a string, bool, or signed long.</span></span> <span data-ttu-id="7d03d-371">Hizmet ifadede bir yerleştirme adlı *kısıtlaması* hizmeti kümedeki burada çalışabilir kısıtlar beri.</span><span class="sxs-lookup"><span data-stu-id="7d03d-371">The statement at the service is called a placement *constraint* since it constrains where the service can run in the cluster.</span></span> <span data-ttu-id="7d03d-372">Kısıtlama kümedeki farklı bir düğüme özelliklerindeki çalışır herhangi bir Boole ifadesini olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-372">The constraint can be any Boolean statement that operates on the different node properties in the cluster.</span></span> <span data-ttu-id="7d03d-373">Bu boolean deyimlerinde geçerli seçiciler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7d03d-373">The valid selectors in these boolean statements are:</span></span>

1) <span data-ttu-id="7d03d-374">belirli ifadeleri oluşturmak için koşullu denetimleri</span><span class="sxs-lookup"><span data-stu-id="7d03d-374">conditional checks for creating particular statements</span></span>

| <span data-ttu-id="7d03d-375">Deyimi</span><span class="sxs-lookup"><span data-stu-id="7d03d-375">Statement</span></span> | <span data-ttu-id="7d03d-376">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7d03d-376">Syntax</span></span> |
| --- |:---:|
| <span data-ttu-id="7d03d-377">"eşit"</span><span class="sxs-lookup"><span data-stu-id="7d03d-377">"equal to"</span></span> | <span data-ttu-id="7d03d-378">"=="</span><span class="sxs-lookup"><span data-stu-id="7d03d-378">"=="</span></span> |
| <span data-ttu-id="7d03d-379">"eşit değil"</span><span class="sxs-lookup"><span data-stu-id="7d03d-379">"not equal to"</span></span> | <span data-ttu-id="7d03d-380">"!="</span><span class="sxs-lookup"><span data-stu-id="7d03d-380">"!="</span></span> |
| <span data-ttu-id="7d03d-381">"büyüktür"</span><span class="sxs-lookup"><span data-stu-id="7d03d-381">"greater than"</span></span> | <span data-ttu-id="7d03d-382">">"</span><span class="sxs-lookup"><span data-stu-id="7d03d-382">">"</span></span> |
| <span data-ttu-id="7d03d-383">"değerinden büyük veya eşit"</span><span class="sxs-lookup"><span data-stu-id="7d03d-383">"greater than or equal to"</span></span> | <span data-ttu-id="7d03d-384">">="</span><span class="sxs-lookup"><span data-stu-id="7d03d-384">">="</span></span> |
| <span data-ttu-id="7d03d-385">"küçüktür"</span><span class="sxs-lookup"><span data-stu-id="7d03d-385">"less than"</span></span> | <span data-ttu-id="7d03d-386">"<"</span><span class="sxs-lookup"><span data-stu-id="7d03d-386">"<"</span></span> |
| <span data-ttu-id="7d03d-387">"küçük veya eşit"</span><span class="sxs-lookup"><span data-stu-id="7d03d-387">"less than or equal to"</span></span> | <span data-ttu-id="7d03d-388">"<="</span><span class="sxs-lookup"><span data-stu-id="7d03d-388">"<="</span></span> |

2) <span data-ttu-id="7d03d-389">gruplandırma ve mantıksal işlemleri için Boole ifadeleri</span><span class="sxs-lookup"><span data-stu-id="7d03d-389">boolean statements for grouping and logical operations</span></span>

| <span data-ttu-id="7d03d-390">Deyimi</span><span class="sxs-lookup"><span data-stu-id="7d03d-390">Statement</span></span> | <span data-ttu-id="7d03d-391">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7d03d-391">Syntax</span></span> |
| --- |:---:|
| <span data-ttu-id="7d03d-392">"ve"</span><span class="sxs-lookup"><span data-stu-id="7d03d-392">"and"</span></span> | <span data-ttu-id="7d03d-393">"&&"</span><span class="sxs-lookup"><span data-stu-id="7d03d-393">"&&"</span></span> |
| <span data-ttu-id="7d03d-394">"veya"</span><span class="sxs-lookup"><span data-stu-id="7d03d-394">"or"</span></span> | <span data-ttu-id="7d03d-395">"&#124;&#124;"</span><span class="sxs-lookup"><span data-stu-id="7d03d-395">"&#124;&#124;"</span></span> |
| <span data-ttu-id="7d03d-396">"değil"</span><span class="sxs-lookup"><span data-stu-id="7d03d-396">"not"</span></span> | <span data-ttu-id="7d03d-397">"!"</span><span class="sxs-lookup"><span data-stu-id="7d03d-397">"!"</span></span> |
| <span data-ttu-id="7d03d-398">"grubu olarak tek bir deyimde"</span><span class="sxs-lookup"><span data-stu-id="7d03d-398">"group as single statement"</span></span> | <span data-ttu-id="7d03d-399">"()"</span><span class="sxs-lookup"><span data-stu-id="7d03d-399">"()"</span></span> |

<span data-ttu-id="7d03d-400">Temel kısıtlama deyimleri bazı örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-400">Here are some examples of basic constraint statements.</span></span>

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

<span data-ttu-id="7d03d-401">Yalnızca genel yerleştirme kısıtlaması deyimi burada "True" olarak değerlendirilir düğümler üzerinde yerleştirilen hizmetine sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d03d-401">Only nodes where the overall placement constraint statement evaluates to “True” can have the service placed on it.</span></span> <span data-ttu-id="7d03d-402">Tanımlanmış bir özellik olmayan düğümleri içeren bu özellik her yerleştirme kısıtlamayla eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="7d03d-402">Nodes that do not have a property defined do not match any placement constraint containing that property.</span></span>

<span data-ttu-id="7d03d-403">Verilen düğüm türü için aşağıdaki düğüm özellikleri tanımlanmadı varsayalım:</span><span class="sxs-lookup"><span data-stu-id="7d03d-403">Let’s say that the following node properties were defined for a given node type:</span></span>

<span data-ttu-id="7d03d-404">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="7d03d-404">ClusterManifest.xml</span></span>

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

<span data-ttu-id="7d03d-405">tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan.</span><span class="sxs-lookup"><span data-stu-id="7d03d-405">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span></span> 

> [!NOTE]
> <span data-ttu-id="7d03d-406">Azure Resource Manager şablonunuzda düğüm türü genellikle parametreli.</span><span class="sxs-lookup"><span data-stu-id="7d03d-406">In your Azure Resource Manager template the node type is usually parameterized.</span></span> <span data-ttu-id="7d03d-407">"NodeType01 yerine", "[parameters('vmNodeType1Name')]" gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="7d03d-407">It would look like "[parameters('vmNodeType1Name')]" rather than "NodeType01".</span></span>
>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

<span data-ttu-id="7d03d-408">Hizmet yerleşimi oluşturabilirsiniz *kısıtlamaları* gösterildiği gibi bir hizmet için:</span><span class="sxs-lookup"><span data-stu-id="7d03d-408">You can create service placement *constraints* for a service like as follows:</span></span>

<span data-ttu-id="7d03d-409">C#</span><span class="sxs-lookup"><span data-stu-id="7d03d-409">C#</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="7d03d-410">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7d03d-410">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

<span data-ttu-id="7d03d-411">Tüm düğümleri NodeType01 geçerliyse, bu düğüm türü kısıtlaması ile öğesini de seçebilirsiniz "(NodeType == NodeType01)".</span><span class="sxs-lookup"><span data-stu-id="7d03d-411">If all nodes of NodeType01 are valid, you can also select that node type with the constraint "(NodeType == NodeType01)".</span></span>

<span data-ttu-id="7d03d-412">Bir hizmetin kısıtlamalarından cool çalışmalarıdır bunlar dinamik olarak çalışma zamanı sırasında güncelleştirilmesi biridir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-412">One of the cool things about a service’s placement constraints is that they can be updated dynamically during runtime.</span></span> <span data-ttu-id="7d03d-413">Bu nedenle gerekiyorsa, kümedeki bir hizmet gezinme, ekleyip kaldırabilirsiniz gereksinimleri, vb.. Service Fabric bile bu tip değişiklikler yapıldığında hizmeti açık ve kullanılabilir kaldığından emin olma mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="7d03d-413">So if you need to, you can move a service around in the cluster, add and remove requirements, etc. Service Fabric takes care of ensuring that the service stays up and available even when these types of changes are made.</span></span>

<span data-ttu-id="7d03d-414">C# ' TA:</span><span class="sxs-lookup"><span data-stu-id="7d03d-414">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

<span data-ttu-id="7d03d-415">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7d03d-415">Powershell:</span></span>

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

<span data-ttu-id="7d03d-416">Kısıtlamalarından her farklı adlı hizmet örneği için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-416">Placement constraints are specified for every different named service instance.</span></span> <span data-ttu-id="7d03d-417">Güncelleştirmeleri her zaman yerini alan (üzerine yaz) ne daha önce belirtildi.</span><span class="sxs-lookup"><span data-stu-id="7d03d-417">Updates always take the place of (overwrite) what was previously specified.</span></span>

<span data-ttu-id="7d03d-418">Küme tanımı bir düğümde özelliklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7d03d-418">The cluster definition defines the properties on a node.</span></span> <span data-ttu-id="7d03d-419">Bir düğümün özelliklerini değiştirme küme yapılandırması yükseltme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-419">Changing a node's properties requires a cluster configuration upgrade.</span></span> <span data-ttu-id="7d03d-420">Bir düğümün özellikleri yükseltme yeni özelliklerini raporlamak için yeniden başlatma için etkilenen her düğüme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-420">Upgrading a node's properties requires each affected node to restart to report its new properties.</span></span> <span data-ttu-id="7d03d-421">Bunlar çalışırken yükseltme Service Fabric tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-421">These rolling upgrades are managed by Service Fabric.</span></span>

## <a name="describing-and-managing-cluster-resources"></a><span data-ttu-id="7d03d-422">Açıklayan ve küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="7d03d-422">Describing and Managing Cluster Resources</span></span>
<span data-ttu-id="7d03d-423">Tüm orchestrator en önemli işlerden biri kümedeki kaynak tüketimini yönetmenize yardımcı olmaktır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-423">One of the most important jobs of any orchestrator is to help manage resource consumption in the cluster.</span></span> <span data-ttu-id="7d03d-424">Küme kaynaklarını yönetme farklı şunları anlamına gelebilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-424">Managing cluster resources can mean a couple of different things.</span></span> <span data-ttu-id="7d03d-425">İlk olarak, var. makineler aşırı yüklü olmadığını sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-425">First, there's ensuring that machines are not overloaded.</span></span> <span data-ttu-id="7d03d-426">Bu makineler bunlar işleyebileceğinden daha fazla hizmet çalıştırmıyor emin olma anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-426">This means making sure that machines aren't running more services than they can handle.</span></span> <span data-ttu-id="7d03d-427">İkinci olarak, Yük Dengeleme ve Hizmetleri verimli bir şekilde çalışmasını için kritik olan en iyi duruma getirme yoktur.</span><span class="sxs-lookup"><span data-stu-id="7d03d-427">Second, there's balancing and optimization which is critical to running services efficiently.</span></span> <span data-ttu-id="7d03d-428">Maliyet etkili veya performans hassas hizmet teklifleri başkalarının soğuk durumdayken etkin olması bazı düğümler izin veremez.</span><span class="sxs-lookup"><span data-stu-id="7d03d-428">Cost effective or performance sensitive service offerings can't allow some nodes to be hot while others are cold.</span></span> <span data-ttu-id="7d03d-429">Kaynak çakışması ve performansın etkin düğümleri sağlama ve soğuk düğümleri harcanan kaynakları ve artan maliyetleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7d03d-429">Hot nodes lead to resource contention and poor performance, and cold nodes represent wasted resources and increased costs.</span></span> 

<span data-ttu-id="7d03d-430">Service Fabric kaynakları olarak temsil eden `Metrics`.</span><span class="sxs-lookup"><span data-stu-id="7d03d-430">Service Fabric represents resources as `Metrics`.</span></span> <span data-ttu-id="7d03d-431">Service Fabric tanımlamak istediğiniz mantıksal veya fiziksel kaynak ölçümleridir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-431">Metrics are any logical or physical resource that you want to describe to Service Fabric.</span></span> <span data-ttu-id="7d03d-432">"WorkQueueDepth" veya "MemoryInMb" gibi şeyleri ölçümleri örnekleridir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-432">Examples of metrics are things like “WorkQueueDepth” or “MemoryInMb”.</span></span> <span data-ttu-id="7d03d-433">Düğümlerde Service Fabric yönetebilecek fiziksel kaynakları hakkında bilgi için bkz: [kaynak İdaresi](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="7d03d-433">For information about the physical resources that Service Fabric can govern on nodes, see [resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="7d03d-434">Özel ölçümleri ve kullanımları yapılandırma hakkında daha fazla bilgi için bkz: [bu makalede](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="7d03d-434">For information on configuring custom metrics and their uses, see [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

<span data-ttu-id="7d03d-435">Ölçümleri yerleşimi kısıtlamaları ve düğüm özellikleri farklıdır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-435">Metrics are different from placements constraints and node properties.</span></span> <span data-ttu-id="7d03d-436">Düğüm, düğümlerin kendilerini statik tanımlayıcıları özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-436">Node properties are static descriptors of the nodes themselves.</span></span> <span data-ttu-id="7d03d-437">Ölçümleri düğümünüz kaynaklar ve bir düğümde çalıştırdığınızda hizmetlerini kullanma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-437">Metrics describe resources that nodes have and that services consume when they are run on a node.</span></span> <span data-ttu-id="7d03d-438">Bir düğüm özelliği "HasSSD" olabilir ve true veya false ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d03d-438">A node property could be "HasSSD" and could be set to true or false.</span></span> <span data-ttu-id="7d03d-439">Kullanılabilir alan miktarını, SSD ve ne kadar hizmetler tarafından kullanılan "DriveSpaceInMb" gibi bir ölçü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-439">The amount of space available on that SSD and how much is consumed by services would be a metric like “DriveSpaceInMb”.</span></span> 

<span data-ttu-id="7d03d-440">Gibi kısıtlamalarından ve düğüm özellikleri için Service Fabric kümesi Kaynak Yöneticisi ölçümleri adlarını anlamı anlamıyor olduğunu dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-440">It is important to note that just like for placement constraints and node properties, the Service Fabric Cluster Resource Manager doesn't understand what the names of the metrics mean.</span></span> <span data-ttu-id="7d03d-441">Ölçüm adları yalnızca dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-441">Metric names are just strings.</span></span> <span data-ttu-id="7d03d-442">Birim belirsiz olabilir, oluşturduğunuz ölçüm adları bir parçası olarak bildirmek için iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-442">It is a good practice to declare units as a part of the metric names that you create when it could be ambiguous.</span></span>

## <a name="capacity"></a><span data-ttu-id="7d03d-443">Kapasite</span><span class="sxs-lookup"><span data-stu-id="7d03d-443">Capacity</span></span>
<span data-ttu-id="7d03d-444">Tüm kaynak etkinleştirdiyseniz *Dengeleme*, Service Fabric'ın Küme Kaynak Yöneticisi hala sağlamak hiçbir düğüm kapasitesi sonuçlandı olduğunu.</span><span class="sxs-lookup"><span data-stu-id="7d03d-444">If you turned off all resource *balancing*, Service Fabric’s Cluster Resource Manager would still ensure that no node ended up over its capacity.</span></span> <span data-ttu-id="7d03d-445">Kapasite taşmaları yönetme küme çok dolu veya iş yükünün düğümlerinden büyük olduğu sürece mümkündür.</span><span class="sxs-lookup"><span data-stu-id="7d03d-445">Managing capacity overruns is possible unless the cluster is too full or the workload is larger than any node.</span></span> <span data-ttu-id="7d03d-446">Kapasitesi ise başka bir *kısıtlaması* Küme Kaynak Yöneticisi'ni düğüm bir kaynağın ne kadarının anlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-446">Capacity is another *constraint* that the Cluster Resource Manager uses to understand how much of a resource a node has.</span></span> <span data-ttu-id="7d03d-447">Kapasite kalan da küme için bir bütün olarak izlenir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-447">Remaining capacity is also tracked for the cluster as a whole.</span></span> <span data-ttu-id="7d03d-448">Kapasite ve hizmet düzeyinde tüketim ölçümleri cinsinden ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-448">Both the capacity and the consumption at the service level are expressed in terms of metrics.</span></span> <span data-ttu-id="7d03d-449">Bu nedenle örneğin ölçüm "ClientConnections" olabilir ve belirli bir düğümün 32768 "ClientConnections" için bir kapasiteye sahip.</span><span class="sxs-lookup"><span data-stu-id="7d03d-449">So for example, the metric might be "ClientConnections" and a given Node may have a capacity for "ClientConnections" of 32768.</span></span> <span data-ttu-id="7d03d-450">Diğer düğümlere o düğümü üzerinde çalıştıran bazı hizmet deyin, şu anda "ClientConnections" ölçüsünün 32256 kullanan diğer sınırlamaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-450">Other nodes can have other limits Some service running on that node can say it is currently consuming 32256 of the metric "ClientConnections".</span></span>

<span data-ttu-id="7d03d-451">Çalışma zamanı sırasında Kalan kapasite kümedeki ve düğümlerdeki Küme Kaynak Yöneticisi'ni izler.</span><span class="sxs-lookup"><span data-stu-id="7d03d-451">During runtime, the Cluster Resource Manager tracks remaining capacity in the cluster and on nodes.</span></span> <span data-ttu-id="7d03d-452">Kapasite izlemek üzere Küme Kaynağı Yöneticisi her hizmetin kullanımı hizmetin çalıştığı düğümün kapasiteden çıkarır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-452">In order to track capacity the Cluster Resource Manager subtracts each service's usage from node's capacity where the service runs.</span></span> <span data-ttu-id="7d03d-453">Bu bilgilerle Service Fabric kümesi Kaynak Yöneticisi yerleştirin veya düğüm kapasitesi geçmez, böylece çoğaltmaları taşımak nereye tahmin.</span><span class="sxs-lookup"><span data-stu-id="7d03d-453">With this information, the Service Fabric Cluster Resource Manager can figure out where to place or move replicas so that nodes don’t go over capacity.</span></span>

<span data-ttu-id="7d03d-454"><center>
![Küme düğümlerini ve kapasite][Image7]
</center></span><span class="sxs-lookup"><span data-stu-id="7d03d-454"><center>
![Cluster nodes and capacity][Image7]
</center></span></span>

<span data-ttu-id="7d03d-455">C# ' TA:</span><span class="sxs-lookup"><span data-stu-id="7d03d-455">C#:</span></span>

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "ClientConnections";
metric.PrimaryDefaultLoad = 1024;
metric.SecondaryDefaultLoad = 0;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="7d03d-456">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7d03d-456">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

<span data-ttu-id="7d03d-457">Küme bildiriminde tanımlanan kapasiteleri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7d03d-457">You can see capacities defined in the cluster manifest:</span></span>

<span data-ttu-id="7d03d-458">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="7d03d-458">ClusterManifest.xml</span></span>

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

<span data-ttu-id="7d03d-459">tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan.</span><span class="sxs-lookup"><span data-stu-id="7d03d-459">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span></span> 

```json
"nodeTypes": [
    {
        "name": "NodeType03",
        "capacities": {
            "ClientConnections": "65536",
        }
    }
],
```

<span data-ttu-id="7d03d-460">Yaygın olarak bir hizmetin değişiklikleri dinamik olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7d03d-460">Commonly a service’s load changes dynamically.</span></span> <span data-ttu-id="7d03d-461">"ClientConnections" yineleme yükünü 1024'ten 2048 değişti, ancak ardından çalıştığı üzerinde düğüm yalnızca bu ölçüm için kalan 512 kapasitesi olduğu söyleyin.</span><span class="sxs-lookup"><span data-stu-id="7d03d-461">Say that a replica's load of "ClientConnections" changed from 1024 to 2048, but the node it was running on then only had 512 capacity remaining for that metric.</span></span> <span data-ttu-id="7d03d-462">Bu düğüm üzerinde yeterli alan olmadığından şimdi bu çoğaltma veya örneğinin yerleştirme, geçersiz.</span><span class="sxs-lookup"><span data-stu-id="7d03d-462">Now that replica or instance's placement is invalid, since there's not enough room on that node.</span></span> <span data-ttu-id="7d03d-463">İlkenin etkisini gösterip ve düğüm kapasitesi aşağıda geri almak Küme Kaynak Yöneticisi'ni vardır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-463">The Cluster Resource Manager has to kick in and get the node back below capacity.</span></span> <span data-ttu-id="7d03d-464">Bir veya daha fazla çoğaltmalar veya örnekleri bu düğümden başka düğümlere taşıyarak kapasite aşımı düğümü üzerindeki yükü azaltır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-464">It reduces load on the node that is over capacity by moving one or more of the replicas or instances from that node to other nodes.</span></span> <span data-ttu-id="7d03d-465">Çoğaltmaları taşırken, bu hareketleri maliyetini en aza indirmek Küme Kaynak Yöneticisi'ni çalışır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-465">When moving replicas, the Cluster Resource Manager tries to minimize the cost of those movements.</span></span> <span data-ttu-id="7d03d-466">Taşıma maliyeti ele alınmıştır [bu makalede](service-fabric-cluster-resource-manager-movement-cost.md) Küme Kaynak Yöneticisi hakkında daha fazla yeniden dengelenmesi stratejilerini ve kurallar açıklanmaktadır [burada](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="7d03d-466">Movement cost is discussed in [this article](service-fabric-cluster-resource-manager-movement-cost.md) and more about the Cluster Resource Manager's rebalancing strategies and rules is described [here](service-fabric-cluster-resource-manager-metrics.md).</span></span>

## <a name="cluster-capacity"></a><span data-ttu-id="7d03d-467">Küme kapasite</span><span class="sxs-lookup"><span data-stu-id="7d03d-467">Cluster capacity</span></span>
<span data-ttu-id="7d03d-468">Service Fabric kümesi Kaynak Yöneticisi çok tam engeller genel küme nasıl tutmak?</span><span class="sxs-lookup"><span data-stu-id="7d03d-468">So how does the Service Fabric Cluster Resource Manager keep the overall cluster from being too full?</span></span> <span data-ttu-id="7d03d-469">İyi yok çok dinamik yük ile bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d03d-469">Well, with dynamic load there’s not a lot it can do.</span></span> <span data-ttu-id="7d03d-470">Küme Kaynak Yöneticisi tarafından gerçekleştirilen eylemler bağımsız olarak kendi yük depo Hizmetleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-470">Services can have their load spike independently of actions taken by the Cluster Resource Manager.</span></span> <span data-ttu-id="7d03d-471">Sonuç olarak, yarın ünlü olduğunda kümenizle yeterli boş alan bugün underpowered olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-471">As a result, your cluster with plenty of headroom today may be underpowered when you become famous tomorrow.</span></span> <span data-ttu-id="7d03d-472">Bu, içinde sorunları önlemek için baked bazı denetimler vardır belirtti.</span><span class="sxs-lookup"><span data-stu-id="7d03d-472">That said, there are some controls that are baked in to prevent problems.</span></span> <span data-ttu-id="7d03d-473">Yapabiliriz ilk şey, kümenin dolmasına neden olur yeni iş yüklerine oluşturulmasını engellemek ' dir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-473">The first thing we can do is prevent the creation of new workloads that would cause the cluster to become full.</span></span>

<span data-ttu-id="7d03d-474">Durum bilgisi olmayan bir hizmet oluşturmak ve onunla ilişkili bazı yük sahip söyleyin.</span><span class="sxs-lookup"><span data-stu-id="7d03d-474">Say that you create a stateless service and it has some load associated with it.</span></span> <span data-ttu-id="7d03d-475">Hizmet hakkında "DiskSpaceInMb" ölçüm cares varsayalım.</span><span class="sxs-lookup"><span data-stu-id="7d03d-475">Let’s say that the service cares about the "DiskSpaceInMb" metric.</span></span> <span data-ttu-id="7d03d-476">Ayrıca hizmet, her örneği için "DiskSpaceInMb" beş birimleri tüketmeye geçiyor olduğunu düşünelim.</span><span class="sxs-lookup"><span data-stu-id="7d03d-476">Let's also say that it is going to consume five units of "DiskSpaceInMb" for every instance of the service.</span></span> <span data-ttu-id="7d03d-477">Üç hizmet örneklerini oluşturmak istiyorum.</span><span class="sxs-lookup"><span data-stu-id="7d03d-477">You want to create three instances of the service.</span></span> <span data-ttu-id="7d03d-478">Harika!</span><span class="sxs-lookup"><span data-stu-id="7d03d-478">Great!</span></span> <span data-ttu-id="7d03d-479">Bu nedenle "Küme bize bile sırada bulunması DiskSpaceInMb" 15 birimleri ihtiyacımız anlamına bu hizmet örnekleri oluşturmak mümkün olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-479">So that means that we need 15 units of "DiskSpaceInMb" to be present in the cluster in order for us to even be able to create these service instances.</span></span> <span data-ttu-id="7d03d-480">Küme Kaynak Yöneticisi'ni sürekli kapasitesi ve her ölçümü tüketimini hesaplar kümedeki kalan kapasite belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d03d-480">The Cluster Resource Manager continually calculates the capacity and consumption of each metric so it can determine the remaining capacity in the cluster.</span></span> <span data-ttu-id="7d03d-481">Yeterli alan yoksa, Küme Kaynak Yöneticisi oluşturma hizmeti çağrısı reddeder.</span><span class="sxs-lookup"><span data-stu-id="7d03d-481">If there isn't enough space, the Cluster Resource Manager rejects the create service call.</span></span>

<span data-ttu-id="7d03d-482">Gereksinim yalnızca 15 birimler kullanılabilir olmadığından, bu alanı birçok farklı yolu ayrılamadı.</span><span class="sxs-lookup"><span data-stu-id="7d03d-482">Since the requirement is only that there be 15 units available, this space could be allocated many different ways.</span></span> <span data-ttu-id="7d03d-483">Örneğin, olabilir bir kalan birim kapasitesi 15 farklı düğümlerde ya da üç kalan birim kapasitesi beş farklı düğümlerde.</span><span class="sxs-lookup"><span data-stu-id="7d03d-483">For example, there could be one remaining unit of capacity on 15 different nodes, or three remaining units of capacity on five different nodes.</span></span> <span data-ttu-id="7d03d-484">Bu yüzden beş birimler kullanılabilir üç düğümlerde küme Kaynak Yöneticisi'ni şeyler düzenleyebilirsiniz hizmeti yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-484">If the Cluster Resource Manager can rearrange things so there's five units available on three nodes, it places the service.</span></span> <span data-ttu-id="7d03d-485">Küme yeniden düzenleme küme dolmak veya mevcut Hizmetleri herhangi bir nedenden dolayı birleştirilmiş olamaz sürece genellikle mümkündür.</span><span class="sxs-lookup"><span data-stu-id="7d03d-485">Rearranging the cluster is usually possible unless the cluster is almost full or the existing services can't be consolidated for some reason.</span></span>

## <a name="buffered-capacity"></a><span data-ttu-id="7d03d-486">Arabelleğe alınan kapasite</span><span class="sxs-lookup"><span data-stu-id="7d03d-486">Buffered Capacity</span></span>
<span data-ttu-id="7d03d-487">Arabelleğe alınan kapasite başka bir küme kaynağı Yöneticisi'nin özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-487">Buffered capacity is another feature of the Cluster Resource Manager.</span></span> <span data-ttu-id="7d03d-488">Bazı genel düğüm kapasitesi kısmının ayırma sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d03d-488">It allows reservation of some portion of the overall node capacity.</span></span> <span data-ttu-id="7d03d-489">Bu kapasite arabellek yalnızca Hizmetleri yükseltme ve düğüm hataları sırasında yerleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-489">This capacity buffer is only used to place services during upgrades and node failures.</span></span> <span data-ttu-id="7d03d-490">Arabelleğe alınan kapasite ölçüm tüm düğümler için başına genel olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-490">Buffered Capacity is specified globally per metric for all nodes.</span></span> <span data-ttu-id="7d03d-491">Ayrılmış kapasiteyi çekme değeri, hata ve yükseltme kümedeki sahip etki alanları sayısı bir işlevdir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-491">The value you pick for the reserved capacity is a function of the number of Fault and Upgrade Domains you have in the cluster.</span></span> <span data-ttu-id="7d03d-492">Daha fazla hata ve yükseltme etki alanları anlamına gelir için arabelleğe alınan kapasite daha düşük bir sayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d03d-492">More Fault and Upgrade Domains means that you can pick a lower number for your buffered capacity.</span></span> <span data-ttu-id="7d03d-493">Daha fazla etki alanı varsa, yükseltmeleri ve hataları sırasında kullanılamaz hale gelmesine kümenizi daha küçük miktarda bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d03d-493">If you have more domains, you can expect smaller amounts of your cluster to be unavailable during upgrades and failures.</span></span> <span data-ttu-id="7d03d-494">Düğüm kapasitesi bir ölçüm için ayrıca belirttiyseniz arabelleğe alınan kapasite belirtme yalnızca anlamlıdır.</span><span class="sxs-lookup"><span data-stu-id="7d03d-494">Specifying Buffered Capacity only makes sense if you have also specified the node capacity for a metric.</span></span>

<span data-ttu-id="7d03d-495">Arabelleğe alınan kapasite belirleme konusunda bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7d03d-495">Here's an example of how to specify buffered capacity:</span></span>

<span data-ttu-id="7d03d-496">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="7d03d-496">ClusterManifest.xml</span></span>

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

<span data-ttu-id="7d03d-497">tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:</span><span class="sxs-lookup"><span data-stu-id="7d03d-497">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "SomeMetric",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

<span data-ttu-id="7d03d-498">Küme bir ölçüm için arabelleğe alınan kapasite dışında olduğunda yeni hizmetler oluşturma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="7d03d-498">The creation of new services fails when the cluster is out of buffered capacity for a metric.</span></span> <span data-ttu-id="7d03d-499">Arabellek korumak için yeni hizmetler oluşturulmasını önleme yükseltmeleri ve hataları kapasite aşımı gitmek düğümleri neden yok sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d03d-499">Preventing the creation of new services to preserve the buffer ensures that upgrades and failures don’t cause nodes to go over capacity.</span></span> <span data-ttu-id="7d03d-500">Arabelleğe alınan kapasite isteğe bağlıdır, ancak bir ölçüm için bir kapasite tanımlayan herhangi bir küme önerilir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-500">Buffered capacity is optional but is recommended in any cluster that defines a capacity for a metric.</span></span>

<span data-ttu-id="7d03d-501">Küme Kaynak Yöneticisi'ni bu yük bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d03d-501">The Cluster Resource Manager exposes this load information.</span></span> <span data-ttu-id="7d03d-502">Her ölçüm için bu bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="7d03d-502">For each metric, this information includes:</span></span> 
  - <span data-ttu-id="7d03d-503">arabelleğe alınan kapasite ayarları</span><span class="sxs-lookup"><span data-stu-id="7d03d-503">the buffered capacity settings</span></span>
  - <span data-ttu-id="7d03d-504">Toplam Kapasite</span><span class="sxs-lookup"><span data-stu-id="7d03d-504">the total capacity</span></span>
  - <span data-ttu-id="7d03d-505">Geçerli tüketim</span><span class="sxs-lookup"><span data-stu-id="7d03d-505">the current consumption</span></span>
  - <span data-ttu-id="7d03d-506">Dengeli veya her ölçümü olup olmadığı kabul edilir</span><span class="sxs-lookup"><span data-stu-id="7d03d-506">whether each metric is considered balanced or not</span></span>
  - <span data-ttu-id="7d03d-507">Standart sapma hakkındaki istatistiklerdir</span><span class="sxs-lookup"><span data-stu-id="7d03d-507">statistics about the standard deviation</span></span>
  - <span data-ttu-id="7d03d-508">en olan düğümler ve en az yükleme</span><span class="sxs-lookup"><span data-stu-id="7d03d-508">the nodes which have the most and least load</span></span>  
  
<span data-ttu-id="7d03d-509">Aşağıdaki örnek, çıktı olarak bakın:</span><span class="sxs-lookup"><span data-stu-id="7d03d-509">Below we see an example of that output:</span></span>

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a><span data-ttu-id="7d03d-510">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7d03d-510">Next steps</span></span>
* <span data-ttu-id="7d03d-511">Mimari ve bilgi akışını içinde Küme Kaynak Yöneticisi hakkında daha fazla bilgi için kullanıma [bu makalede](service-fabric-cluster-resource-manager-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="7d03d-511">For information on the architecture and information flow within the Cluster Resource Manager, check out [this article ](service-fabric-cluster-resource-manager-architecture.md)</span></span>
* <span data-ttu-id="7d03d-512">Birleştirme ölçümleri tanımlama yayılmak yerine düğümlerde yük birleştirmek için bir yoludur. Birleştirme yapılandırma konusunda bilgi edinmek için bkz [bu makalede](service-fabric-cluster-resource-manager-defragmentation-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="7d03d-512">Defining Defragmentation Metrics is one way to consolidate load on nodes instead of spreading it out. To learn how to configure defragmentation, refer to [this article](service-fabric-cluster-resource-manager-defragmentation-metrics.md)</span></span>
* <span data-ttu-id="7d03d-513">En baştan başlatın ve [bir giriş için Service Fabric kümesi Resource Manager Al](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="7d03d-513">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
* <span data-ttu-id="7d03d-514">Küme Kaynak Yöneticisi'ni yönetir ve yük devretme kümesinde dengeleyen hakkında bilgi almak için makalesine kontrol [Yük Dengeleme](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="7d03d-514">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
