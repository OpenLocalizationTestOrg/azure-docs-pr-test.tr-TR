---
title: "aaaManage işlem güç Azure SQL Data warehouse'da (genel bakış) | Microsoft Docs"
description: "Azure SQL veri ambarı özellikleri genişletme performans. Dwu ayarlayarak ölçeğini veya duraklatma ve işlem kaynakları toosave maliyetlerini sürdürme."
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
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="31bdc-104">Azure SQL Data warehouse'da (genel bakış) işlem güç yönetimi</span><span class="sxs-lookup"><span data-stu-id="31bdc-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31bdc-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="31bdc-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="31bdc-106">Portal</span><span class="sxs-lookup"><span data-stu-id="31bdc-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="31bdc-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31bdc-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="31bdc-108">REST</span><span class="sxs-lookup"><span data-stu-id="31bdc-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="31bdc-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="31bdc-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="31bdc-110">SQL veri ambarı Hello mimarisi, depolama ve işlem, her tooscale bağımsız olarak izin verme ayırır.</span><span class="sxs-lookup"><span data-stu-id="31bdc-110">hello architecture of SQL Data Warehouse separates storage and compute, allowing each tooscale independently.</span></span> <span data-ttu-id="31bdc-111">Sonuç olarak, işlem ölçeklendirilmiş toomeet performans taleplerini hello veri miktarını bağımsız olabilir.</span><span class="sxs-lookup"><span data-stu-id="31bdc-111">As a result, compute can be scaled toomeet performance demands independent of hello amount of data.</span></span> <span data-ttu-id="31bdc-112">Bu mimarinin doğal bir sonuç [fatura] [ billed] işlem ve depolama için ayrıdır.</span><span class="sxs-lookup"><span data-stu-id="31bdc-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="31bdc-113">Bu genel bakış açıklanmaktadır nasıl ölçeğini SQL veri ambarı ve tooutilize nasıl hello duraklatma, sürdürme ve SQL Data Warehouse ölçek özelliklerini çalışır.</span><span class="sxs-lookup"><span data-stu-id="31bdc-113">This overview describes how scale out works with SQL Data Warehouse and how tooutilize hello pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="31bdc-114">Merhaba başvurun [veri ambarı birimlerini (Dwu'lar)] [ data warehouse units (DWUs)] sayfa toolearn nasıl Dwu ve performans ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="31bdc-114">Consult hello [data warehouse units (DWUs)][data warehouse units (DWUs)] page toolearn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="31bdc-115">SQL veri ambarı'nda yönetim işlemlerini iş nasıl işlem</span><span class="sxs-lookup"><span data-stu-id="31bdc-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="31bdc-116">Merhaba mimarisi SQL veri ambarı için bir denetim düğümü oluşur, işlem düğümleri ve 60 dağıtımları yayılan hello depolama katmanı.</span><span class="sxs-lookup"><span data-stu-id="31bdc-116">hello architecture for SQL Data Warehouse consists of a control node, compute nodes, and hello storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="31bdc-117">Normal etkin oturum SQL Data warehouse'da sırasında sisteminizin baş düğüm hello meta verileri yönetir ve hello dağıtılmış sorgu iyileştiricisi içerir.</span><span class="sxs-lookup"><span data-stu-id="31bdc-117">During a normal active session in SQL Data Warehouse, your system's head node manages hello metadata and contains hello distributed query optimizer.</span></span> <span data-ttu-id="31bdc-118">Bu baş düğümü altında işlem düğümlerini ve depolama katmanı olan.</span><span class="sxs-lookup"><span data-stu-id="31bdc-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="31bdc-119">DWU 400 için sisteminizi bir baş düğüm, dört işlem düğümlerini ve 60 dağıtımlarını oluşan hello depolama katmanı vardır.</span><span class="sxs-lookup"><span data-stu-id="31bdc-119">For a DWU 400, your system has one head node, four compute nodes, and hello storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="31bdc-120">Bir ölçek uygulanabilecek veya işlemi duraklatmak, hello sistem ilk tüm gelen sorguları sonlandırır ve işlemleri tooensure tutarlı bir duruma geri alınır.</span><span class="sxs-lookup"><span data-stu-id="31bdc-120">When you undergo a scale or pause operation, hello system first kills all incoming queries and then rolls back transactions tooensure a consistent state.</span></span> <span data-ttu-id="31bdc-121">Bu işlem geri alma işlemi tamamlandıktan sonra ölçek işlemleri için ölçeklendirme yalnızca meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="31bdc-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="31bdc-122">Bir ölçek büyütme işleminin hello sistem hükümleri fazladan istenen işlem düğümleri sayısını hello ve hello işlem düğümleri toohello depolama katmanı yeniden takmanız başlar.</span><span class="sxs-lookup"><span data-stu-id="31bdc-122">For a scale-up operation, hello system provisions hello extra desired number of compute nodes, and then begins reattaching hello compute nodes toohello storage layer.</span></span> <span data-ttu-id="31bdc-123">Bir ölçek azaltma işlemi için hello gereksiz düğümleri yayımlanan ve hello kalan işlem düğümleri kendilerini dağıtımları uygun sayıda toohello yeniden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="31bdc-123">For a scale-down operation, hello unneeded nodes are released and hello remaining compute nodes reattach themselves toohello appropriate number of distributions.</span></span> <span data-ttu-id="31bdc-124">Duraklatma işlemi için tüm düğümler yayımlanan ve sisteminizin meta veri işlemleri tooleave çeşitli son kararlı bir duruma sisteminizdeki yapılacaktır işlem.</span><span class="sxs-lookup"><span data-stu-id="31bdc-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations tooleave your final system in a stable state.</span></span>

| <span data-ttu-id="31bdc-125">DWU</span><span class="sxs-lookup"><span data-stu-id="31bdc-125">DWU</span></span>  | <span data-ttu-id="31bdc-126">\#işlem düğümleri</span><span class="sxs-lookup"><span data-stu-id="31bdc-126">\#of compute nodes</span></span> | <span data-ttu-id="31bdc-127">\#Düğüm başına dağıtımları</span><span class="sxs-lookup"><span data-stu-id="31bdc-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="31bdc-128">100</span><span class="sxs-lookup"><span data-stu-id="31bdc-128">100</span></span>  | <span data-ttu-id="31bdc-129">1</span><span class="sxs-lookup"><span data-stu-id="31bdc-129">1</span></span>                  | <span data-ttu-id="31bdc-130">60</span><span class="sxs-lookup"><span data-stu-id="31bdc-130">60</span></span>                           |
| <span data-ttu-id="31bdc-131">200</span><span class="sxs-lookup"><span data-stu-id="31bdc-131">200</span></span>  | <span data-ttu-id="31bdc-132">2</span><span class="sxs-lookup"><span data-stu-id="31bdc-132">2</span></span>                  | <span data-ttu-id="31bdc-133">30</span><span class="sxs-lookup"><span data-stu-id="31bdc-133">30</span></span>                           |
| <span data-ttu-id="31bdc-134">300</span><span class="sxs-lookup"><span data-stu-id="31bdc-134">300</span></span>  | <span data-ttu-id="31bdc-135">3</span><span class="sxs-lookup"><span data-stu-id="31bdc-135">3</span></span>                  | <span data-ttu-id="31bdc-136">20</span><span class="sxs-lookup"><span data-stu-id="31bdc-136">20</span></span>                           |
| <span data-ttu-id="31bdc-137">400</span><span class="sxs-lookup"><span data-stu-id="31bdc-137">400</span></span>  | <span data-ttu-id="31bdc-138">4</span><span class="sxs-lookup"><span data-stu-id="31bdc-138">4</span></span>                  | <span data-ttu-id="31bdc-139">15</span><span class="sxs-lookup"><span data-stu-id="31bdc-139">15</span></span>                           |
| <span data-ttu-id="31bdc-140">500</span><span class="sxs-lookup"><span data-stu-id="31bdc-140">500</span></span>  | <span data-ttu-id="31bdc-141">5</span><span class="sxs-lookup"><span data-stu-id="31bdc-141">5</span></span>                  | <span data-ttu-id="31bdc-142">12</span><span class="sxs-lookup"><span data-stu-id="31bdc-142">12</span></span>                           |
| <span data-ttu-id="31bdc-143">600</span><span class="sxs-lookup"><span data-stu-id="31bdc-143">600</span></span>  | <span data-ttu-id="31bdc-144">6</span><span class="sxs-lookup"><span data-stu-id="31bdc-144">6</span></span>                  | <span data-ttu-id="31bdc-145">10</span><span class="sxs-lookup"><span data-stu-id="31bdc-145">10</span></span>                           |
| <span data-ttu-id="31bdc-146">1000</span><span class="sxs-lookup"><span data-stu-id="31bdc-146">1000</span></span> | <span data-ttu-id="31bdc-147">10</span><span class="sxs-lookup"><span data-stu-id="31bdc-147">10</span></span>                 | <span data-ttu-id="31bdc-148">6</span><span class="sxs-lookup"><span data-stu-id="31bdc-148">6</span></span>                            |
| <span data-ttu-id="31bdc-149">1200</span><span class="sxs-lookup"><span data-stu-id="31bdc-149">1200</span></span> | <span data-ttu-id="31bdc-150">12</span><span class="sxs-lookup"><span data-stu-id="31bdc-150">12</span></span>                 | <span data-ttu-id="31bdc-151">5</span><span class="sxs-lookup"><span data-stu-id="31bdc-151">5</span></span>                            |
| <span data-ttu-id="31bdc-152">1500</span><span class="sxs-lookup"><span data-stu-id="31bdc-152">1500</span></span> | <span data-ttu-id="31bdc-153">15</span><span class="sxs-lookup"><span data-stu-id="31bdc-153">15</span></span>                 | <span data-ttu-id="31bdc-154">4</span><span class="sxs-lookup"><span data-stu-id="31bdc-154">4</span></span>                            |
| <span data-ttu-id="31bdc-155">2000</span><span class="sxs-lookup"><span data-stu-id="31bdc-155">2000</span></span> | <span data-ttu-id="31bdc-156">20</span><span class="sxs-lookup"><span data-stu-id="31bdc-156">20</span></span>                 | <span data-ttu-id="31bdc-157">3</span><span class="sxs-lookup"><span data-stu-id="31bdc-157">3</span></span>                            |
| <span data-ttu-id="31bdc-158">3000</span><span class="sxs-lookup"><span data-stu-id="31bdc-158">3000</span></span> | <span data-ttu-id="31bdc-159">30</span><span class="sxs-lookup"><span data-stu-id="31bdc-159">30</span></span>                 | <span data-ttu-id="31bdc-160">2</span><span class="sxs-lookup"><span data-stu-id="31bdc-160">2</span></span>                            |
| <span data-ttu-id="31bdc-161">6000</span><span class="sxs-lookup"><span data-stu-id="31bdc-161">6000</span></span> | <span data-ttu-id="31bdc-162">60</span><span class="sxs-lookup"><span data-stu-id="31bdc-162">60</span></span>                 | <span data-ttu-id="31bdc-163">1</span><span class="sxs-lookup"><span data-stu-id="31bdc-163">1</span></span>                            |

<span data-ttu-id="31bdc-164">işlem yönetmek için hello üç birincil işlev şunlardır:</span><span class="sxs-lookup"><span data-stu-id="31bdc-164">hello three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="31bdc-165">Duraklat</span><span class="sxs-lookup"><span data-stu-id="31bdc-165">Pause</span></span>
2. <span data-ttu-id="31bdc-166">Sürdür</span><span class="sxs-lookup"><span data-stu-id="31bdc-166">Resume</span></span>
3. <span data-ttu-id="31bdc-167">Ölçek</span><span class="sxs-lookup"><span data-stu-id="31bdc-167">Scale</span></span>

<span data-ttu-id="31bdc-168">Bu işlemlerin her biri, birkaç dakika toocomplete devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="31bdc-168">Each of these operations may take several minutes toocomplete.</span></span> <span data-ttu-id="31bdc-169">Otomatik olarak ölçeklendirme/duraklatma/sürdürme varsa, tooimplement mantığı tooensure başka bir eylem işlemine devam etmeden önce işlem tamamlandığında, belirli isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31bdc-169">If you are scaling/pausing/resuming automatically, you may want tooimplement logic tooensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="31bdc-170">Çeşitli uç noktaları aracılığıyla Hello veritabanı durumunu denetleme toocorrectly uygulama Otomasyon böyle işlemlerinin izin verir.</span><span class="sxs-lookup"><span data-stu-id="31bdc-170">Checking hello database state through various endpoints will allow you toocorrectly implement automation of such operations.</span></span> <span data-ttu-id="31bdc-171">Merhaba portalı bir işlemi ve hello veritabanları geçerli durumu tamamlanmasından sonra bildirim sağlar ancak programlı durumunu denetlemek için izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="31bdc-171">hello portal will provide notification upon completion of an operation and hello databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="31bdc-172">İşlem yönetimi işlevselliği tüm uç noktalar arasında yok.</span><span class="sxs-lookup"><span data-stu-id="31bdc-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="31bdc-173">Duraklat/Sürdür</span><span class="sxs-lookup"><span data-stu-id="31bdc-173">Pause/Resume</span></span> | <span data-ttu-id="31bdc-174">Ölçek</span><span class="sxs-lookup"><span data-stu-id="31bdc-174">Scale</span></span> | <span data-ttu-id="31bdc-175">Veritabanı durumunu kontrol edin</span><span class="sxs-lookup"><span data-stu-id="31bdc-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="31bdc-176">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="31bdc-176">Azure portal</span></span> | <span data-ttu-id="31bdc-177">Evet</span><span class="sxs-lookup"><span data-stu-id="31bdc-177">Yes</span></span>          | <span data-ttu-id="31bdc-178">Evet</span><span class="sxs-lookup"><span data-stu-id="31bdc-178">Yes</span></span>   | <span data-ttu-id="31bdc-179">**Hayır**</span><span class="sxs-lookup"><span data-stu-id="31bdc-179">**No**</span></span>               |
| <span data-ttu-id="31bdc-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31bdc-180">PowerShell</span></span>   | <span data-ttu-id="31bdc-181">Evet</span><span class="sxs-lookup"><span data-stu-id="31bdc-181">Yes</span></span>          | <span data-ttu-id="31bdc-182">Evet</span><span class="sxs-lookup"><span data-stu-id="31bdc-182">Yes</span></span>   | <span data-ttu-id="31bdc-183">Evet</span><span class="sxs-lookup"><span data-stu-id="31bdc-183">Yes</span></span>                  |
| <span data-ttu-id="31bdc-184">REST API</span><span class="sxs-lookup"><span data-stu-id="31bdc-184">REST API</span></span>     | <span data-ttu-id="31bdc-185">Evet</span><span class="sxs-lookup"><span data-stu-id="31bdc-185">Yes</span></span>          | <span data-ttu-id="31bdc-186">Evet</span><span class="sxs-lookup"><span data-stu-id="31bdc-186">Yes</span></span>   | <span data-ttu-id="31bdc-187">Evet</span><span class="sxs-lookup"><span data-stu-id="31bdc-187">Yes</span></span>                  |
| <span data-ttu-id="31bdc-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="31bdc-188">T-SQL</span></span>        | <span data-ttu-id="31bdc-189">**Hayır**</span><span class="sxs-lookup"><span data-stu-id="31bdc-189">**No**</span></span>       | <span data-ttu-id="31bdc-190">Evet</span><span class="sxs-lookup"><span data-stu-id="31bdc-190">Yes</span></span>   | <span data-ttu-id="31bdc-191">Evet</span><span class="sxs-lookup"><span data-stu-id="31bdc-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="31bdc-192">Bilgi işlem</span><span class="sxs-lookup"><span data-stu-id="31bdc-192">Scale compute</span></span>

<span data-ttu-id="31bdc-193">SQL veri ambarı performans ölçülür [veri ambarı birimlerini (Dwu'lar)] [ data warehouse units (DWUs)] CPU, bellek ve g/ç bant genişliği gibi işlem kaynakları abstracted bir ölçü değil.</span><span class="sxs-lookup"><span data-stu-id="31bdc-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="31bdc-194">Kendi sistem performansını tooscale isteyen bir kullanıcı çeşitli yollarla gibi hello portal, T-SQL ve REST API'leri bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31bdc-194">A user who wishes tooscale their system's performance can do so through various means, such as through hello portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="31bdc-195">İşlem nasıl ölçeklendirme?</span><span class="sxs-lookup"><span data-stu-id="31bdc-195">How do I scale compute?</span></span>
<span data-ttu-id="31bdc-196">İşlem gücü, SQL Data Warehouse hello DWU ayarını değiştirerek yönetilir.</span><span class="sxs-lookup"><span data-stu-id="31bdc-196">Compute power is managed for you SQL Data Warehouse by changing hello DWU setting.</span></span> <span data-ttu-id="31bdc-197">Performans artışı [doğrusal olarak] [ linearly] gibi belirli işlemler için daha fazla DWU ekleyin.</span><span class="sxs-lookup"><span data-stu-id="31bdc-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="31bdc-198">Yukarı veya aşağı sisteminizi ne zaman ölçeklendirme, performansı belirgin şekilde değişir olun DWU teklifleri sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="31bdc-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="31bdc-199">tooadjust Dwu, tek tek bu yöntemlerden birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31bdc-199">tooadjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="31bdc-200">[Azure portal ile güç işlem ölçeklendirme][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="31bdc-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="31bdc-201">[İşlem PowerShell ile güç ölçeklendirme][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="31bdc-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="31bdc-202">[REST API'leri ile ölçek işlem gücü][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="31bdc-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="31bdc-203">[TSQL ile güç işlem ölçeklendirme][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="31bdc-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="31bdc-204">Kaç tane Dwu kullanmalıyım?</span><span class="sxs-lookup"><span data-stu-id="31bdc-204">How many DWUs should I use?</span></span>

<span data-ttu-id="31bdc-205">hangi, ideal DWU değerdir, toounderstand yukarı ve aşağı doğru ölçeklendirme ve verilerinizi yükledikten sonra birkaç sorgu çalıştırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="31bdc-205">toounderstand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="31bdc-206">Ölçeklendirme hızla gerçekleştiği bir saat veya daha az çeşitli performans düzeylerini deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31bdc-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="31bdc-207">SQL veri ambarı tasarlanmış tooprocess büyük miktarlarda verinin ' dir.</span><span class="sxs-lookup"><span data-stu-id="31bdc-207">SQL Data Warehouse is designed tooprocess large amounts of data.</span></span> <span data-ttu-id="31bdc-208">toosee, özellikle büyük Dwu ölçeklendirmeye yönelik gerçek kapasitesini istediğiniz toouse, 1 TB yaklaşıyor veya büyük bir veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="31bdc-208">toosee its true capabilities for scaling, especially at larger DWUs, you want toouse a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="31bdc-209">Bulma için öneriler, iş yükü için en iyi DWU hello:</span><span class="sxs-lookup"><span data-stu-id="31bdc-209">Recommendations for finding hello best DWU for your workload:</span></span>

1. <span data-ttu-id="31bdc-210">Geliştirme bir veri ambarı için daha küçük bir DWU performans düzeyi seçerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="31bdc-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="31bdc-211">İyi bir başlangıç noktası DW400 veya DW200 ' dir.</span><span class="sxs-lookup"><span data-stu-id="31bdc-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="31bdc-212">Uygulama performansı izleme, seçili Dwu sayısı hello Gözlemleme, gözlemlemek toohello performans karşılaştırılan.</span><span class="sxs-lookup"><span data-stu-id="31bdc-212">Monitor your application performance, observing hello number of DWUs selected compared toohello performance you observe.</span></span>
3. <span data-ttu-id="31bdc-213">Ne kadar hızlı veya daha yavaş performans, tooreach hello en iyi performansı düzeyi için gereksinimlerinizi doğrusal ölçek üstlenerek olacağını belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31bdc-213">Determine how much faster or slower performance should be for you tooreach hello optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="31bdc-214">Artırma veya azaltma hello numarası oranı toohow çok daha hızlı veya daha yavaş Dwu, iş yükü tooperform istiyor.</span><span class="sxs-lookup"><span data-stu-id="31bdc-214">Increase or decrease hello number of DWUs in proportion toohow much faster or slower you want your workload tooperform.</span></span> 
5. <span data-ttu-id="31bdc-215">İş gereksinimleriniz için en iyi performansı düzeyi ulaşana kadar ayarlamaları devam edin.</span><span class="sxs-lookup"><span data-stu-id="31bdc-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="31bdc-216">Merhaba iş işlem düğümleri arasında bölünebilir, sorgu performansı ile daha fazla paralelleştirme yalnızca artırır.</span><span class="sxs-lookup"><span data-stu-id="31bdc-216">Query performance only increases with more parallelization if hello work can be split between compute nodes.</span></span> <span data-ttu-id="31bdc-217">Ölçeklendirme performansınızı değişmeyen olduğunu fark ederseniz, lütfen bizim performans makaleleri toocheck verilerinizi düz olmayan şekilde dağıtılmış olup olmadığını veya çok miktarda veri taşıma giriş varsa ayarlama denetleyin.</span><span class="sxs-lookup"><span data-stu-id="31bdc-217">If you find that scaling is not changing your performance, please check out our performance tuning articles toocheck whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="31bdc-218">Dwu zaman ölçeklendirmeniz gerekir?</span><span class="sxs-lookup"><span data-stu-id="31bdc-218">When should I scale DWUs?</span></span>
<span data-ttu-id="31bdc-219">Dwu ölçeklendirme önemli senaryolar aşağıdaki hello değiştirir:</span><span class="sxs-lookup"><span data-stu-id="31bdc-219">Scaling DWUs alters hello following important scenarios:</span></span>

1. <span data-ttu-id="31bdc-220">Doğrusal olarak taramaları, toplamalar ve CTAS deyimleri hello sistem performansını değiştirme</span><span class="sxs-lookup"><span data-stu-id="31bdc-220">Linearly changing performance of hello system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="31bdc-221">PolyBase ile birlikte yüklenirken okuyucuları ve yazıcıları Hello sayısını artırmayı</span><span class="sxs-lookup"><span data-stu-id="31bdc-221">Increasing hello number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="31bdc-222">Maksimum eş zamanlı sorgular ve eşzamanlılık yuva sayısı</span><span class="sxs-lookup"><span data-stu-id="31bdc-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="31bdc-223">Ne zaman için öneriler tooscale Dwu:</span><span class="sxs-lookup"><span data-stu-id="31bdc-223">Recommendations for when tooscale DWUs:</span></span>

1. <span data-ttu-id="31bdc-224">Çok miktarda verinin yüklendiği veya dönüştürüldüğü işlemi gerçekleştirmeden önce verilerinizin daha hızlı kullanılabilir olmasını sağlamak Dwu ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="31bdc-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="31bdc-225">Yoğun iş saatlerinde tooaccommodate çok sayıda eş zamanlı sorguları ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="31bdc-225">During peak business hours, scale tooaccommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="31bdc-226">Duraklatma işlem</span><span class="sxs-lookup"><span data-stu-id="31bdc-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="31bdc-227">bir veritabanı toopause tek tek bu yöntemlerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="31bdc-227">toopause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="31bdc-228">[Azure portal ile Duraklat işlem][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="31bdc-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="31bdc-229">[PowerShell ile Duraklat işlem][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="31bdc-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="31bdc-230">[REST API'leri ile Duraklat işlem][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="31bdc-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="31bdc-231">Resume işlem</span><span class="sxs-lookup"><span data-stu-id="31bdc-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="31bdc-232">bir veritabanı tooresume tek tek bu yöntemlerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="31bdc-232">tooresume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="31bdc-233">[Azure portal ile Sürdür işlem][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="31bdc-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="31bdc-234">[PowerShell ile Sürdür işlem][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="31bdc-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="31bdc-235">[REST API'leri ile Sürdür işlem][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="31bdc-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="31bdc-236">Veritabanı durumunu kontrol edin</span><span class="sxs-lookup"><span data-stu-id="31bdc-236">Check database state</span></span> 

<span data-ttu-id="31bdc-237">bir veritabanı tooresume tek tek bu yöntemlerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="31bdc-237">tooresume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="31bdc-238">[T-SQL ile veritabanı durumunu kontrol edin][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="31bdc-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="31bdc-239">[PowerShell ile veritabanı durumunu kontrol edin][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="31bdc-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="31bdc-240">[REST API'leri ile veritabanı durumunu kontrol edin][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="31bdc-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="31bdc-241">İzinler</span><span class="sxs-lookup"><span data-stu-id="31bdc-241">Permissions</span></span>

<span data-ttu-id="31bdc-242">Ölçeklendirme hello veritabanı açıklanan hello izinleri gerektirir [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="31bdc-242">Scaling hello database requires hello permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="31bdc-243">Duraklatma ve sürdürme gerektiren hello [SQL DB Katılımcısı] [ SQL DB Contributor] izni, özellikle Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="31bdc-243">Pause and Resume require hello [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="31bdc-244">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="31bdc-244">Next steps</span></span>
<span data-ttu-id="31bdc-245">Bazı ek anahtar performans kavramları anlamanız makaleleri toohelp aşağıdaki toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="31bdc-245">Refer toohello following articles toohelp you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="31bdc-246">[İş yükü ve eşzamanlılık Yönetimi][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="31bdc-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="31bdc-247">[Tablo Tasarım genel bakış][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="31bdc-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="31bdc-248">[Tablo dağıtım][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="31bdc-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="31bdc-249">[Tablo dizin oluşturma][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="31bdc-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="31bdc-250">[Tablo bölümleme][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="31bdc-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="31bdc-251">[Tablo istatistikleri][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="31bdc-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="31bdc-252">[En iyi uygulamalar][Best practices]</span><span class="sxs-lookup"><span data-stu-id="31bdc-252">[Best practices][Best practices]</span></span>

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
