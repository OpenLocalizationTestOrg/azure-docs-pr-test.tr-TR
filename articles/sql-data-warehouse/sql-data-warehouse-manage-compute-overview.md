---
title: "Azure SQL Data warehouse'da (genel bakış) işlem güç yönetimi | Microsoft Docs"
description: "Azure SQL veri ambarı özellikleri genişletme performans. Dwu ayarlayarak ölçeğini veya duraklatıp işlem kaynakları maliyet tasarrufu sağlamak."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: abe22f542a79714f6e894870872ee6b76ffe7633
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="a7b8e-104">Azure SQL Data warehouse'da (genel bakış) işlem güç yönetimi</span><span class="sxs-lookup"><span data-stu-id="a7b8e-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7b8e-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a7b8e-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="a7b8e-106">Portal</span><span class="sxs-lookup"><span data-stu-id="a7b8e-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="a7b8e-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7b8e-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="a7b8e-108">REST</span><span class="sxs-lookup"><span data-stu-id="a7b8e-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="a7b8e-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="a7b8e-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="a7b8e-110">SQL Data Warehouse mimarisi, depolama ve işlem, her bağımsız olarak ölçeklendirebilirsiniz izin vererek ayırır.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-110">The architecture of SQL Data Warehouse separates storage and compute, allowing each to scale independently.</span></span> <span data-ttu-id="a7b8e-111">Sonuç olarak, işlem veri miktarını bağımsız performans taleplerini karşılamak üzere genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-111">As a result, compute can be scaled to meet performance demands independent of the amount of data.</span></span> <span data-ttu-id="a7b8e-112">Bu mimarinin doğal bir sonuç [fatura] [ billed] işlem ve depolama için ayrıdır.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="a7b8e-113">Bu genel bakış açıklanmaktadır SQL veri ambarı ve Duraklat kullanmaya nasıl çalışır nasıl ölçeğini sürdürme ve ölçeklendirme SQL veri ambarı özelliklerini.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-113">This overview describes how scale out works with SQL Data Warehouse and how to utilize the pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="a7b8e-114">Başvurun [veri ambarı birimlerini (Dwu'lar)] [ data warehouse units (DWUs)] Dwu ve performans nasıl ilişkili olduğunu öğrenmek için sayfa.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-114">Consult the [data warehouse units (DWUs)][data warehouse units (DWUs)] page to learn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="a7b8e-115">SQL veri ambarı'nda yönetim işlemlerini iş nasıl işlem</span><span class="sxs-lookup"><span data-stu-id="a7b8e-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="a7b8e-116">Bir denetim düğümü, işlem düğümlerini ve 60 dağıtımları yayılan depolama katmanı, SQL Data Warehouse mimarisi oluşur.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-116">The architecture for SQL Data Warehouse consists of a control node, compute nodes, and the storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="a7b8e-117">Normal etkin oturum SQL Data warehouse'da sırasında sisteminizin baş düğüm meta verileri yönetir ve dağıtılmış sorgu iyileştiricisi içerir.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-117">During a normal active session in SQL Data Warehouse, your system's head node manages the metadata and contains the distributed query optimizer.</span></span> <span data-ttu-id="a7b8e-118">Bu baş düğümü altında işlem düğümlerini ve depolama katmanı olan.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="a7b8e-119">DWU 400 için sisteminizi bir baş düğüm, dört işlem düğümlerini ve 60 dağıtımlarını oluşan depolama katmanı vardır.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-119">For a DWU 400, your system has one head node, four compute nodes, and the storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="a7b8e-120">Bir ölçek uygulanabilecek veya işlemi duraklatmak, sistem önce tüm gelen sorguları sonlandırır ve tutarlı bir duruma emin olmak için işlemler geri alınır.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-120">When you undergo a scale or pause operation, the system first kills all incoming queries and then rolls back transactions to ensure a consistent state.</span></span> <span data-ttu-id="a7b8e-121">Bu işlem geri alma işlemi tamamlandıktan sonra ölçek işlemleri için ölçeklendirme yalnızca meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="a7b8e-122">Bir ölçek büyütme işleminin ek sayısı istenen sistem hükümleri işlem düğümleri ve depolama katmanı için işlem düğümleri yeniden takmanız başlar.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-122">For a scale-up operation, the system provisions the extra desired number of compute nodes, and then begins reattaching the compute nodes to the storage layer.</span></span> <span data-ttu-id="a7b8e-123">Bir ölçek azaltma işlemi için gereksiz düğümleri yayımlanan ve geri kalan işlem düğümleri kendilerini uygun sayıda dağıtımlar için yeniden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-123">For a scale-down operation, the unneeded nodes are released and the remaining compute nodes reattach themselves to the appropriate number of distributions.</span></span> <span data-ttu-id="a7b8e-124">Duraklatma işlemi için tüm düğümler yayımlanan ve sisteminizin meta veri işlemleri, son sistem kararlı durumda bırakın, çeşitli yapılacaktır işlem.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations to leave your final system in a stable state.</span></span>

| <span data-ttu-id="a7b8e-125">DWU</span><span class="sxs-lookup"><span data-stu-id="a7b8e-125">DWU</span></span>  | <span data-ttu-id="a7b8e-126">\#işlem düğümleri</span><span class="sxs-lookup"><span data-stu-id="a7b8e-126">\#of compute nodes</span></span> | <span data-ttu-id="a7b8e-127">\#Düğüm başına dağıtımları</span><span class="sxs-lookup"><span data-stu-id="a7b8e-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="a7b8e-128">100</span><span class="sxs-lookup"><span data-stu-id="a7b8e-128">100</span></span>  | <span data-ttu-id="a7b8e-129">1</span><span class="sxs-lookup"><span data-stu-id="a7b8e-129">1</span></span>                  | <span data-ttu-id="a7b8e-130">60</span><span class="sxs-lookup"><span data-stu-id="a7b8e-130">60</span></span>                           |
| <span data-ttu-id="a7b8e-131">200</span><span class="sxs-lookup"><span data-stu-id="a7b8e-131">200</span></span>  | <span data-ttu-id="a7b8e-132">2</span><span class="sxs-lookup"><span data-stu-id="a7b8e-132">2</span></span>                  | <span data-ttu-id="a7b8e-133">30</span><span class="sxs-lookup"><span data-stu-id="a7b8e-133">30</span></span>                           |
| <span data-ttu-id="a7b8e-134">300</span><span class="sxs-lookup"><span data-stu-id="a7b8e-134">300</span></span>  | <span data-ttu-id="a7b8e-135">3</span><span class="sxs-lookup"><span data-stu-id="a7b8e-135">3</span></span>                  | <span data-ttu-id="a7b8e-136">20</span><span class="sxs-lookup"><span data-stu-id="a7b8e-136">20</span></span>                           |
| <span data-ttu-id="a7b8e-137">400</span><span class="sxs-lookup"><span data-stu-id="a7b8e-137">400</span></span>  | <span data-ttu-id="a7b8e-138">4</span><span class="sxs-lookup"><span data-stu-id="a7b8e-138">4</span></span>                  | <span data-ttu-id="a7b8e-139">15</span><span class="sxs-lookup"><span data-stu-id="a7b8e-139">15</span></span>                           |
| <span data-ttu-id="a7b8e-140">500</span><span class="sxs-lookup"><span data-stu-id="a7b8e-140">500</span></span>  | <span data-ttu-id="a7b8e-141">5</span><span class="sxs-lookup"><span data-stu-id="a7b8e-141">5</span></span>                  | <span data-ttu-id="a7b8e-142">12</span><span class="sxs-lookup"><span data-stu-id="a7b8e-142">12</span></span>                           |
| <span data-ttu-id="a7b8e-143">600</span><span class="sxs-lookup"><span data-stu-id="a7b8e-143">600</span></span>  | <span data-ttu-id="a7b8e-144">6</span><span class="sxs-lookup"><span data-stu-id="a7b8e-144">6</span></span>                  | <span data-ttu-id="a7b8e-145">10</span><span class="sxs-lookup"><span data-stu-id="a7b8e-145">10</span></span>                           |
| <span data-ttu-id="a7b8e-146">1000</span><span class="sxs-lookup"><span data-stu-id="a7b8e-146">1000</span></span> | <span data-ttu-id="a7b8e-147">10</span><span class="sxs-lookup"><span data-stu-id="a7b8e-147">10</span></span>                 | <span data-ttu-id="a7b8e-148">6</span><span class="sxs-lookup"><span data-stu-id="a7b8e-148">6</span></span>                            |
| <span data-ttu-id="a7b8e-149">1200</span><span class="sxs-lookup"><span data-stu-id="a7b8e-149">1200</span></span> | <span data-ttu-id="a7b8e-150">12</span><span class="sxs-lookup"><span data-stu-id="a7b8e-150">12</span></span>                 | <span data-ttu-id="a7b8e-151">5</span><span class="sxs-lookup"><span data-stu-id="a7b8e-151">5</span></span>                            |
| <span data-ttu-id="a7b8e-152">1500</span><span class="sxs-lookup"><span data-stu-id="a7b8e-152">1500</span></span> | <span data-ttu-id="a7b8e-153">15</span><span class="sxs-lookup"><span data-stu-id="a7b8e-153">15</span></span>                 | <span data-ttu-id="a7b8e-154">4</span><span class="sxs-lookup"><span data-stu-id="a7b8e-154">4</span></span>                            |
| <span data-ttu-id="a7b8e-155">2000</span><span class="sxs-lookup"><span data-stu-id="a7b8e-155">2000</span></span> | <span data-ttu-id="a7b8e-156">20</span><span class="sxs-lookup"><span data-stu-id="a7b8e-156">20</span></span>                 | <span data-ttu-id="a7b8e-157">3</span><span class="sxs-lookup"><span data-stu-id="a7b8e-157">3</span></span>                            |
| <span data-ttu-id="a7b8e-158">3000</span><span class="sxs-lookup"><span data-stu-id="a7b8e-158">3000</span></span> | <span data-ttu-id="a7b8e-159">30</span><span class="sxs-lookup"><span data-stu-id="a7b8e-159">30</span></span>                 | <span data-ttu-id="a7b8e-160">2</span><span class="sxs-lookup"><span data-stu-id="a7b8e-160">2</span></span>                            |
| <span data-ttu-id="a7b8e-161">6000</span><span class="sxs-lookup"><span data-stu-id="a7b8e-161">6000</span></span> | <span data-ttu-id="a7b8e-162">60</span><span class="sxs-lookup"><span data-stu-id="a7b8e-162">60</span></span>                 | <span data-ttu-id="a7b8e-163">1</span><span class="sxs-lookup"><span data-stu-id="a7b8e-163">1</span></span>                            |

<span data-ttu-id="a7b8e-164">İşlem yönetmek için üç birincil işlev şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a7b8e-164">The three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="a7b8e-165">Duraklat</span><span class="sxs-lookup"><span data-stu-id="a7b8e-165">Pause</span></span>
2. <span data-ttu-id="a7b8e-166">Sürdür</span><span class="sxs-lookup"><span data-stu-id="a7b8e-166">Resume</span></span>
3. <span data-ttu-id="a7b8e-167">Ölçek</span><span class="sxs-lookup"><span data-stu-id="a7b8e-167">Scale</span></span>

<span data-ttu-id="a7b8e-168">Bu işlemlerin her biri tamamlanması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-168">Each of these operations may take several minutes to complete.</span></span> <span data-ttu-id="a7b8e-169">Otomatik olarak ölçeklendirme/duraklatma/sürdürme varsa, belirli işlemleri başka bir eylem işlemine devam etmeden önce tamamlandığından emin olmak için mantığı uygulamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-169">If you are scaling/pausing/resuming automatically, you may want to implement logic to ensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="a7b8e-170">Çeşitli uç noktaları aracılığıyla veritabanı durumunu denetleme doğru Otomasyon böyle işlemlerinin uygulamaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-170">Checking the database state through various endpoints will allow you to correctly implement automation of such operations.</span></span> <span data-ttu-id="a7b8e-171">Portal bir işlem ve veritabanlarını tamamlanmasından sonra bildirimi geçerli durumu sağlar ancak programlı durumunu denetlemek için izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-171">The portal will provide notification upon completion of an operation and the databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="a7b8e-172">İşlem yönetimi işlevselliği tüm uç noktalar arasında yok.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="a7b8e-173">Duraklat/Sürdür</span><span class="sxs-lookup"><span data-stu-id="a7b8e-173">Pause/Resume</span></span> | <span data-ttu-id="a7b8e-174">Ölçek</span><span class="sxs-lookup"><span data-stu-id="a7b8e-174">Scale</span></span> | <span data-ttu-id="a7b8e-175">Veritabanı durumunu kontrol edin</span><span class="sxs-lookup"><span data-stu-id="a7b8e-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="a7b8e-176">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="a7b8e-176">Azure portal</span></span> | <span data-ttu-id="a7b8e-177">Evet</span><span class="sxs-lookup"><span data-stu-id="a7b8e-177">Yes</span></span>          | <span data-ttu-id="a7b8e-178">Evet</span><span class="sxs-lookup"><span data-stu-id="a7b8e-178">Yes</span></span>   | <span data-ttu-id="a7b8e-179">**Hayır**</span><span class="sxs-lookup"><span data-stu-id="a7b8e-179">**No**</span></span>               |
| <span data-ttu-id="a7b8e-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7b8e-180">PowerShell</span></span>   | <span data-ttu-id="a7b8e-181">Evet</span><span class="sxs-lookup"><span data-stu-id="a7b8e-181">Yes</span></span>          | <span data-ttu-id="a7b8e-182">Evet</span><span class="sxs-lookup"><span data-stu-id="a7b8e-182">Yes</span></span>   | <span data-ttu-id="a7b8e-183">Evet</span><span class="sxs-lookup"><span data-stu-id="a7b8e-183">Yes</span></span>                  |
| <span data-ttu-id="a7b8e-184">REST API</span><span class="sxs-lookup"><span data-stu-id="a7b8e-184">REST API</span></span>     | <span data-ttu-id="a7b8e-185">Evet</span><span class="sxs-lookup"><span data-stu-id="a7b8e-185">Yes</span></span>          | <span data-ttu-id="a7b8e-186">Evet</span><span class="sxs-lookup"><span data-stu-id="a7b8e-186">Yes</span></span>   | <span data-ttu-id="a7b8e-187">Evet</span><span class="sxs-lookup"><span data-stu-id="a7b8e-187">Yes</span></span>                  |
| <span data-ttu-id="a7b8e-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="a7b8e-188">T-SQL</span></span>        | <span data-ttu-id="a7b8e-189">**Hayır**</span><span class="sxs-lookup"><span data-stu-id="a7b8e-189">**No**</span></span>       | <span data-ttu-id="a7b8e-190">Evet</span><span class="sxs-lookup"><span data-stu-id="a7b8e-190">Yes</span></span>   | <span data-ttu-id="a7b8e-191">Evet</span><span class="sxs-lookup"><span data-stu-id="a7b8e-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="a7b8e-192">Bilgi işlem</span><span class="sxs-lookup"><span data-stu-id="a7b8e-192">Scale compute</span></span>

<span data-ttu-id="a7b8e-193">SQL veri ambarı performans ölçülür [veri ambarı birimlerini (Dwu'lar)] [ data warehouse units (DWUs)] CPU, bellek ve g/ç bant genişliği gibi işlem kaynakları abstracted bir ölçü değil.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="a7b8e-194">Kendi sistem performansını ölçeklendirme istediği bir kullanıcı çeşitli yollarla gibi portalı, T-SQL ve REST API'leri bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-194">A user who wishes to scale their system's performance can do so through various means, such as through the portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="a7b8e-195">İşlem nasıl ölçeklendirme?</span><span class="sxs-lookup"><span data-stu-id="a7b8e-195">How do I scale compute?</span></span>
<span data-ttu-id="a7b8e-196">Güç sizin için SQL Data Warehouse DWU ayarını değiştirerek yönetilen işlem.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-196">Compute power is managed for you SQL Data Warehouse by changing the DWU setting.</span></span> <span data-ttu-id="a7b8e-197">Performans artışı [doğrusal olarak] [ linearly] gibi belirli işlemler için daha fazla DWU ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="a7b8e-198">Yukarı veya aşağı sisteminizi ne zaman ölçeklendirme, performansı belirgin şekilde değişir olun DWU teklifleri sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="a7b8e-199">Dwu ayarlamak için tek tek bu yöntemlerden birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-199">To adjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="a7b8e-200">[Azure portal ile güç işlem ölçeklendirme][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="a7b8e-201">[İşlem PowerShell ile güç ölçeklendirme][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="a7b8e-202">[REST API'leri ile ölçek işlem gücü][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="a7b8e-203">[TSQL ile güç işlem ölçeklendirme][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="a7b8e-204">Kaç tane Dwu kullanmalıyım?</span><span class="sxs-lookup"><span data-stu-id="a7b8e-204">How many DWUs should I use?</span></span>

<span data-ttu-id="a7b8e-205">İdeal DWU değerinizin ne olduğunu anlamak için verilerinizi yükledikten sonra ölçeği artırmayı veya azaltmayı ve birkaç sorgu çalıştırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-205">To understand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="a7b8e-206">Ölçeklendirme hızla gerçekleştiği bir saat veya daha az çeşitli performans düzeylerini deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="a7b8e-207">SQL veri ambarı büyük miktarda veriyi işlemek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-207">SQL Data Warehouse is designed to process large amounts of data.</span></span> <span data-ttu-id="a7b8e-208">Özellikle büyük Dwu ölçeklendirmeye yönelik gerçek kapasitesini görmek için 1 TB yaklaşıyor veya büyük bir veri kümesini kullanmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-208">To see its true capabilities for scaling, especially at larger DWUs, you want to use a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="a7b8e-209">İş yükü için en iyi DWU bulmak için öneriler:</span><span class="sxs-lookup"><span data-stu-id="a7b8e-209">Recommendations for finding the best DWU for your workload:</span></span>

1. <span data-ttu-id="a7b8e-210">Geliştirme bir veri ambarı için daha küçük bir DWU performans düzeyi seçerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="a7b8e-211">İyi bir başlangıç noktası DW400 veya DW200 ' dir.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="a7b8e-212">Uygulama performansı izleme, karşılaştırıldığında, gözlemlemek performans Dwu sayısı seçili gözlemleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-212">Monitor your application performance, observing the number of DWUs selected compared to the performance you observe.</span></span>
3. <span data-ttu-id="a7b8e-213">Doğrusal ölçek üstlenerek gereksinimleriniz için en iyi performans düzeyine ulaşmak size ne kadar hızlı veya daha yavaş performans olacağını belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-213">Determine how much faster or slower performance should be for you to reach the optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="a7b8e-214">Artırın veya azaltın nasıl çok daha hızlı veya daha yavaş gerçekleştirmek için İş yükünüzün istediğiniz orantılı olarak Dwu sayısı.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-214">Increase or decrease the number of DWUs in proportion to how much faster or slower you want your workload to perform.</span></span> 
5. <span data-ttu-id="a7b8e-215">İş gereksinimleriniz için en iyi performansı düzeyi ulaşana kadar ayarlamaları devam edin.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="a7b8e-216">İş işlem düğümleri arasında bölünebilir, sorgu performansı ile daha fazla paralelleştirme yalnızca artırır.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-216">Query performance only increases with more parallelization if the work can be split between compute nodes.</span></span> <span data-ttu-id="a7b8e-217">Ölçeklendirme performansınızı değişmeyen olduğunu fark ederseniz, lütfen bizim performans verilerinizi düz olmayan şekilde dağıtılmış olup olmadığını veya çok miktarda veri taşıma giriş varsa denetlemek için makaleleri ayarlama denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-217">If you find that scaling is not changing your performance, please check out our performance tuning articles to check whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="a7b8e-218">Dwu zaman ölçeklendirmeniz gerekir?</span><span class="sxs-lookup"><span data-stu-id="a7b8e-218">When should I scale DWUs?</span></span>
<span data-ttu-id="a7b8e-219">Dwu ölçeklendirme, aşağıdaki önemli senaryolar değiştirir:</span><span class="sxs-lookup"><span data-stu-id="a7b8e-219">Scaling DWUs alters the following important scenarios:</span></span>

1. <span data-ttu-id="a7b8e-220">Doğrusal olarak taramaları, toplamalar ve CTAS deyimleri için sistem performansını değiştirme</span><span class="sxs-lookup"><span data-stu-id="a7b8e-220">Linearly changing performance of the system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="a7b8e-221">PolyBase ile birlikte yüklenirken okuyucuları ve yazıcıları sayısını artırmayı</span><span class="sxs-lookup"><span data-stu-id="a7b8e-221">Increasing the number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="a7b8e-222">Maksimum eş zamanlı sorgular ve eşzamanlılık yuva sayısı</span><span class="sxs-lookup"><span data-stu-id="a7b8e-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="a7b8e-223">Zaman Dwu ölçeklemek önerileri:</span><span class="sxs-lookup"><span data-stu-id="a7b8e-223">Recommendations for when to scale DWUs:</span></span>

1. <span data-ttu-id="a7b8e-224">Çok miktarda verinin yüklendiği veya dönüştürüldüğü işlemi gerçekleştirmeden önce verilerinizin daha hızlı kullanılabilir olmasını sağlamak Dwu ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="a7b8e-225">Yoğun iş saatlerinde sayıda eş zamanlı sorguları uyacak şekilde ölçeklendirilir.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-225">During peak business hours, scale to accommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="a7b8e-226">Duraklatma işlem</span><span class="sxs-lookup"><span data-stu-id="a7b8e-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="a7b8e-227">Bir veritabanı duraklatmak için tek tek bu yöntemlerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-227">To pause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="a7b8e-228">[Azure portal ile Duraklat işlem][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="a7b8e-229">[PowerShell ile Duraklat işlem][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="a7b8e-230">[REST API'leri ile Duraklat işlem][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="a7b8e-231">Resume işlem</span><span class="sxs-lookup"><span data-stu-id="a7b8e-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="a7b8e-232">Bir veritabanı sürdürmek için tek tek bu yöntemlerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-232">To resume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="a7b8e-233">[Azure portal ile Sürdür işlem][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="a7b8e-234">[PowerShell ile Sürdür işlem][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="a7b8e-235">[REST API'leri ile Sürdür işlem][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="a7b8e-236">Veritabanı durumunu kontrol edin</span><span class="sxs-lookup"><span data-stu-id="a7b8e-236">Check database state</span></span> 

<span data-ttu-id="a7b8e-237">Bir veritabanı sürdürmek için tek tek bu yöntemlerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-237">To resume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="a7b8e-238">[T-SQL ile veritabanı durumunu kontrol edin][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="a7b8e-239">[PowerShell ile veritabanı durumunu kontrol edin][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="a7b8e-240">[REST API'leri ile veritabanı durumunu kontrol edin][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="a7b8e-241">İzinler</span><span class="sxs-lookup"><span data-stu-id="a7b8e-241">Permissions</span></span>

<span data-ttu-id="a7b8e-242">Veritabanı ölçeklendirme açıklanan izinleri gerektirir [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="a7b8e-242">Scaling the database requires the permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="a7b8e-243">Duraklatma ve sürdürme gerektiren [SQL DB Katılımcısı] [ SQL DB Contributor] izni, özellikle Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="a7b8e-243">Pause and Resume require the [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="a7b8e-244">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7b8e-244">Next steps</span></span>
<span data-ttu-id="a7b8e-245">Bazı ek anahtar performans kavramlarını anlamanıza yardımcı olması için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="a7b8e-245">Refer to the following articles to help you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="a7b8e-246">[İş yükü ve eşzamanlılık Yönetimi][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="a7b8e-247">[Tablo Tasarım genel bakış][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="a7b8e-248">[Tablo dağıtım][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="a7b8e-249">[Tablo dizin oluşturma][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="a7b8e-250">[Tablo bölümleme][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="a7b8e-251">[Tablo istatistikleri][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="a7b8e-252">[En iyi uygulamalar][Best practices]</span><span class="sxs-lookup"><span data-stu-id="a7b8e-252">[Best practices][Best practices]</span></span>

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
